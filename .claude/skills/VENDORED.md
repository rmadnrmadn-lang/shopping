# 외부 스킬 출처

이 디렉터리의 일부 스킬은 외부 저장소에서 가져온 것이다. 업스트림 갱신 시 아래 커밋과 대조한다.

| 스킬 | 출처 | 라이선스 | 고정 커밋 |
|---|---|---|---|
| `watch` | https://github.com/bradautomates/claude-video | MIT (Bradley Bonanno) | `83da59fa78c3eee9e20f515fe75c438bb5166efd` (2026-06-30) |
| `remotion-motion-graphics` | https://github.com/haidrrrry/claude-remotion-skill | MIT (haidrrrry) | `1dcbe5e3fc6cf970bd10d3cc05f0a8a5d19d0383` |
| `shopping-shorts` | 이 저장소에서 작성 | — | — |

## watch 런타임 요구사항

`ffmpeg` / `ffprobe` / `yt-dlp`가 필요하다. 컨테이너는 세션마다 초기화되므로 새 세션에서 다시 설치한다:

```bash
pip install yt-dlp
apt-get update -qq && apt-get install -y ffmpeg
```

전사(transcript)는 네이티브 캡션을 먼저 쓰고, 없으면 Whisper API로 넘어간다.
Whisper를 쓰려면 `~/.config/watch/.env`에 `GROQ_API_KEY` 또는 `OPENAI_API_KEY`를 넣는다.
키가 없어도 동작하지만 캡션 없는 영상은 프레임만 나온다.

## 알려진 제약

이 환경의 이그레스 정책이 `tiktok.com`을 차단한다. `yt-dlp`도 프록시에서 403을 받으므로
**TikTok 영상은 watch 스킬로도 받을 수 없다.** 환경 네트워크 정책에서 허용하거나,
영상 파일을 직접 넣어야 한다 (로컬 파일은 정상 동작).
