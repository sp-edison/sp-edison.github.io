---
title: 시뮬레이션 재실행
tags: [EDISON, rerun, workbench]
keywords:
summary: "저장된 시뮬레이션 중 실행했던 것과 동일한 파라미터와 파일들을 기반으로 다시 시뮬레이션을 실행해보고 싶다면, 과거 실행에서 사용했던 파라미터와 파일들을 그대로 가져와서 워크벤치 기반 시뮬레이션을 실행합니다. "
sidebar: user_sidebar
permalink: user_data_rerun.html
folder: user_data
---

## 시뮬레이션 재실행
저장된 시뮬레이션 중에서 실행했던 것과 동일한 파라미터와 파일들을 기반으로 다시 시뮬레이션을 실행해보고 싶은 경우가 있습니다. EDISON 플랫폼은 과거 실행에서 사용했던 파라미터와 파일들을 그대로 가져와서 워크벤치 기반으로 시뮬레이션을 재실행하는 기능을 제공합니다.

- EDISON 플랫폼에서 저장된 시뮬레이션을 확인합니다.

{% include image.html file="data/user_data_rerun_01.png" caption="Surf dataset" %}

- 시뮬레이션 중 실행 당시 사용했던 파라미터와 파일로 재실행해보고 싶은 시뮬레이션이 있다면, 해당 시뮬레이션 페이지에서 `Rerun simulation` 버튼을 누릅니다.

{% include image.html file="data/user_data_rerun_02.png" caption="Rerun simulation" %}

- `Rerun simulation` 버튼을 누르면 실행 시 사용했던 파라미터와 파일들을 가져와서 워크벤치 페이지로 이동합니다.

{% include image.html file="data/user_data_rerun_03.png" caption="Workbench" %}

- 동일한 파라미터와 파일을 그대로 사용하거나, 다른 값으로 수정하여 시뮬레이션 재실행이 가능합니다.
