# Claude Code Deep Dive Workshop

[![Live](https://img.shields.io/badge/Live-CloudFront-orange.svg)](https://d2vlczg32rt5xd.cloudfront.net)
[![Version](https://img.shields.io/badge/Version-2026.07-green.svg)]()
<a href="#english"><img src="https://img.shields.io/badge/lang-English-blue.svg" alt="English"></a>
<a href="#korean"><img src="https://img.shields.io/badge/lang-한국어-red.svg" alt="Korean"></a>

Hands-on workshop site for Claude Code: 5 core chapters plus 3 capstone missions. | Claude Code 핸즈온 워크샵 사이트: 코어 5개 챕터와 캡스톤 미션 3종으로 구성됩니다.

---

<a id="english"></a>

# English

## Overview

Static workshop site that bundles eight hands-on labs into a single "Claude Code Deep Dive Workshop". A hub page (`index.html`) presents the curriculum as a numbered rail that forks into three selectable capstone missions, tracks per-lab completion in `localStorage`, and every lab page carries a floating navigation widget (home / previous / next) that follows the workshop order.

**Live site:** https://d2vlczg32rt5xd.cloudfront.net

The site is served from a private S3 bucket through CloudFront (Origin Access Control, HTTPS only).

## Features

- **Workshop hub** — Curriculum overview with a numbered chapter rail, capstone fork, and per-card completion toggles persisted in the browser
- **Reordered core track** — Labs run in the sequence Ch1 → Ch5 → Ch4 → Ch2 → Ch3, then fork into a capstone of choice
- **Floating lab navigation** — Every lab page links back to the hub and to the previous/next lab in workshop order
- **Zero-backend progress tracking** — Completion state lives in `localStorage`; no server required
- **CloudFront delivery** — Private S3 origin with OAC, HTTPS redirect, Gzip/Brotli compression, HTTP/2+3

## Curriculum

### Core track (run in this order)

| Step | Chapter | Title | Duration | Tasks | Description |
|------|---------|-------|----------|-------|-------------|
| 01 | Ch1 | [Claude Code, from install to headless automation](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch1_HandsOnLab.html) | 40 min | Prep + 6 | Install and authenticate Claude Code, fix a real bug, then run a headless automation pipeline |
| 02 | Ch5 | [CLI Reference, Claude Code as a pipeline component](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch5_HandsOnLab.html) | 40 min | Prep + 4 | Turn the interactive tool into an automation component using the CLI reference in real pipelines |
| 03 | Ch4 | [Settings, from personal tool to team platform](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch4_HandsOnLab.html) | 80 min | 4 Tasks + 4 Missions | Two parts: Part A covers settings, Part B is a super-lab that scales Claude Code into a team platform |
| 04 | Ch2 | [Subagents, build and command specialist agents](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch2_HandsOnLab.html) | 40 min | Prep + 5 | Create code-reviewer, test-writer, and docs-writer subagents and orchestrate them in one task |
| 05 | Ch3 | [Admin Setup, controlled enterprise deployment](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch3_HandsOnLab.html) | 40 min | Prep + 5 | The administrator's 40 minutes: internal npm mirror and policy settings for a controlled rollout |

### Capstone missions (choose one)

| Mission | Title | Theme | Duration | Description |
|---------|-------|-------|----------|-------------|
| A | [Mission: Ship It](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Capstone_HandsOnLab.html) | The Claude that builds | 135 min (cap 150) | Deploy your own Claude Ops Center to AWS as a full-stack exercise with the superpowers plugin |
| B | [Mission: Self-Heal](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_CapstoneB_HandsOnLab_Type2.html) | The Claude that protects | 135 min (cap 150) | Build an unattended operations room: a self-healing SRE agent with a headless medic and safety interlocks |
| C | [Mission: Grand Open](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_CapstoneC_HandsOnLab3.html) | The Claude that sells | 135 min (cap 150) | Open an AI cafe that takes orders in natural language: a customer-service full stack on Sonnet 5 / Opus 4.8 (Global CRIS) |

Lab environment: Claude Code on EC2 with an Admin account, region `ap-northeast-2`, baseline Claude Code 2.1.x.

## Prerequisites

- A modern web browser (the site is fully static)
- For deployment updates: AWS CLI v2 with credentials for account `501520444434`

## Installation

```bash
# Clone the repository
git clone https://github.com/comeddy/claude-web.git
cd claude-web

# Serve locally (optional)
python3 -m http.server 8000
# Open http://localhost:8000
```

## Usage

```bash
# Visit the live site
open https://d2vlczg32rt5xd.cloudfront.net

# Publish content changes
aws s3 sync . s3://claude-code-workshop-501520444434-apne2/ \
  --exclude "*" --include "*.html" \
  --content-type "text/html; charset=utf-8"

# Invalidate the CloudFront cache
aws cloudfront create-invalidation \
  --distribution-id E2P7Q4PMLORNXM --paths "/*"
```

## Project Structure

```
claude-web/
  index.html                                  # Workshop hub (curriculum, progress tracking)
  ClaudeCode_Ch1_HandsOnLab.html              # Step 01 - Overview lab
  ClaudeCode_Ch5_HandsOnLab.html              # Step 02 - CLI Reference lab
  ClaudeCode_Ch4_HandsOnLab.html              # Step 03 - Settings lab (extended)
  ClaudeCode_Ch2_HandsOnLab.html              # Step 04 - Subagents lab
  ClaudeCode_Ch3_HandsOnLab.html              # Step 05 - Admin Setup lab
  ClaudeCode_Capstone_HandsOnLab.html         # Capstone A - Ship It
  ClaudeCode_CapstoneB_HandsOnLab_Type2.html  # Capstone B - Self-Heal
  ClaudeCode_CapstoneC_HandsOnLab3.html       # Capstone C - Grand Open
```

## Contributing

```
1. Fork the repository
2. Create your branch (`git checkout -b feat/amazing-feature`)
3. Commit changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feat/amazing-feature`)
5. Open a Pull Request
```

## License

No open-source license has been applied. This repository is intended for workshop use.

## Contact

- Maintainer: [comeddy](https://github.com/comeddy)
- Issues: https://github.com/comeddy/claude-web/issues

---

<a id="korean"></a>

# 한국어

## 개요

8개의 핸즈온 랩을 하나의 "Claude Code Deep Dive Workshop"으로 묶은 정적 워크샵 사이트입니다. 허브 페이지(`index.html`)는 커리큘럼을 번호가 매겨진 레일로 보여주고, 레일 끝에서 3개의 캡스톤 미션 중 하나를 선택하도록 갈라집니다. 랩별 완료 상태는 `localStorage`에 저장되며, 모든 랩 페이지에는 워크샵 순서를 따르는 플로팅 내비게이션(목차 / 이전 / 다음)이 있습니다.

**라이브 사이트:** https://d2vlczg32rt5xd.cloudfront.net

사이트는 프라이빗 S3 버킷에서 CloudFront(Origin Access Control, HTTPS 전용)를 통해 서빙됩니다.

## 주요 기능

- **워크샵 허브** — 번호 레일 형태의 커리큘럼 개요, 캡스톤 분기, 브라우저에 저장되는 카드별 완료 토글 제공
- **재구성된 코어 트랙** — Ch1 → Ch5 → Ch4 → Ch2 → Ch3 순서로 진행 후 캡스톤 택 1로 분기
- **플로팅 랩 내비게이션** — 모든 랩 페이지에서 허브와 워크샵 순서상 이전/다음 랩으로 이동 가능
- **백엔드 없는 진행률 추적** — 완료 상태를 `localStorage`에 저장하므로 서버가 필요 없음
- **CloudFront 배포** — OAC 기반 프라이빗 S3 오리진, HTTPS 리다이렉트, Gzip/Brotli 압축, HTTP/2+3

## 커리큘럼

### 코어 트랙 (이 순서로 진행)

| 순서 | 챕터 | 제목 | 소요 시간 | Task | 설명 |
|------|------|------|-----------|------|------|
| 01 | Ch1 | [Claude Code, 설치부터 Headless 자동화까지](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch1_HandsOnLab.html) | 40분 | 준비 + 6 | Claude Code를 설치·인증하고 실제 버그를 고친 뒤 Headless 자동화 파이프라인을 실행합니다 |
| 02 | Ch5 | [CLI Reference, Claude Code를 파이프라인의 부품으로](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch5_HandsOnLab.html) | 40분 | 준비 + 4 | CLI 레퍼런스를 활용해 대화 도구를 실전 파이프라인의 자동화 부품으로 전환합니다 |
| 03 | Ch4 | [Settings, 나의 Claude Code를 팀의 플랫폼으로](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch4_HandsOnLab.html) | 80분 | 4 Task + 4 Mission | 2부 구성으로, Part A는 설정 실습, Part B는 팀 플랫폼으로 확장하는 슈퍼랩입니다 |
| 04 | Ch2 | [Subagents, 전문 에이전트를 만들고 지휘하기](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch2_HandsOnLab.html) | 40분 | 준비 + 5 | code-reviewer, test-writer, docs-writer 서브에이전트를 만들어 하나의 작업에서 지휘합니다 |
| 05 | Ch3 | [Admin Setup, 통제 가능한 Enterprise 배포](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Ch3_HandsOnLab.html) | 40분 | 준비 + 5 | 관리자의 40분으로, 사내 npm 미러와 정책 설정으로 통제 가능한 배포를 구성합니다 |

### 캡스톤 미션 (택 1)

| 미션 | 제목 | 테마 | 소요 시간 | 설명 |
|------|------|------|-----------|------|
| A | [Mission: Ship It](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_Capstone_HandsOnLab.html) | 만드는 Claude | 135분 (상한 150분) | superpowers 플러그인과 함께 나의 Claude Ops Center를 AWS에 풀스택으로 배포합니다 |
| B | [Mission: Self-Heal](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_CapstoneB_HandsOnLab_Type2.html) | 지키는 Claude | 135분 (상한 150분) | Headless 메딕과 안전 인터록으로 스스로 복구하는 SRE 에이전트, 무인 운영실을 구축합니다 |
| C | [Mission: Grand Open](https://d2vlczg32rt5xd.cloudfront.net/ClaudeCode_CapstoneC_HandsOnLab3.html) | 파는 Claude | 135분 (상한 150분) | 말로 주문받는 AI 카페를 개점합니다. Sonnet 5 / Opus 4.8 (Global CRIS) 기반 고객 서비스 풀스택입니다 |

랩 환경: Claude Code on EC2 + Admin 계정, 리전 `ap-northeast-2`, 기준 버전 Claude Code 2.1.x.

## 사전 요구 사항

- 최신 웹 브라우저 (사이트는 완전한 정적 페이지입니다)
- 배포 업데이트 시: 계정 `501520444434` 자격 증명이 설정된 AWS CLI v2

## 설치 방법

```bash
# Clone the repository
git clone https://github.com/comeddy/claude-web.git
cd claude-web

# Serve locally (optional)
python3 -m http.server 8000
# Open http://localhost:8000
```

## 사용법

```bash
# Visit the live site
open https://d2vlczg32rt5xd.cloudfront.net

# Publish content changes
aws s3 sync . s3://claude-code-workshop-501520444434-apne2/ \
  --exclude "*" --include "*.html" \
  --content-type "text/html; charset=utf-8"

# Invalidate the CloudFront cache
aws cloudfront create-invalidation \
  --distribution-id E2P7Q4PMLORNXM --paths "/*"
```

## 프로젝트 구조

```
claude-web/
  index.html                                  # 워크샵 허브 (커리큘럼, 진행률 추적)
  ClaudeCode_Ch1_HandsOnLab.html              # 순서 01 - Overview 랩
  ClaudeCode_Ch5_HandsOnLab.html              # 순서 02 - CLI Reference 랩
  ClaudeCode_Ch4_HandsOnLab.html              # 순서 03 - Settings 랩 (확장판)
  ClaudeCode_Ch2_HandsOnLab.html              # 순서 04 - Subagents 랩
  ClaudeCode_Ch3_HandsOnLab.html              # 순서 05 - Admin Setup 랩
  ClaudeCode_Capstone_HandsOnLab.html         # 캡스톤 A - Ship It
  ClaudeCode_CapstoneB_HandsOnLab_Type2.html  # 캡스톤 B - Self-Heal
  ClaudeCode_CapstoneC_HandsOnLab3.html       # 캡스톤 C - Grand Open
```

## 기여 방법

```
1. Fork the repository
2. Create your branch (`git checkout -b feat/amazing-feature`)
3. Commit changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feat/amazing-feature`)
5. Open a Pull Request
```

## 라이선스

오픈소스 라이선스가 적용되지 않았습니다. 이 저장소는 워크샵 용도로 사용됩니다.

## 연락처

- 메인테이너: [comeddy](https://github.com/comeddy)
- 이슈: https://github.com/comeddy/claude-web/issues
