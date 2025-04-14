---
title: RustDesk Client
weight: 2
pre: "<b>1. </b>"
---

### 소개
RustDesk 클라이언트를 통해 오픈소스 또는 Pro RustDesk 서버로 디바이스를 연결할 수 있습니다.
[GitHub](https://git서b.com/rustdesk/rustdesk/releases/latest)에서 다운로드받을 수 있습니다.

### 지원 플랫폼
- Microsoft Windows
- macOS
- Debian 계열 (Ubuntu ≥ 16, Linux Mint 등)
- Red Hat 계열 (CentOS, Fedora ≥ 18, Rocky Linux 등)
- Arch Linux/Manjaro
- openSUSE
- NixOS
- AppImage / Flatpak
- Android
- iOS (제어받는 장치로는 사용할 수 없습니다)
- Web

### 설치 

#### Windows

GitHub에서 exe 파일을 받아 설치하세요.

조용히 설치를 원하신다면, 설치파일을 `--silent-install`과 함께 실행하세요.

#### macOS

GitHub에서 dmg 파일을 다운로드받으세요. 더 많은 정보는 [macOS page](https://rustdesk.com/docs/en/client/mac/)를 참고하세요.

dmg 파일을 열고, `RustDesk`를 `Application`로 드래그하세요.

RustDesk의 실행을 허용해주세요.

요청 권한설정을 허용해주시고, RustDesk의 왼쪽에 표시되는 항목에 따라 설정을 완료해주세요.

#### Linux

배포판에 따라 아래 내용을 참고해주세요. (설치 파일은 GitHub, 혹은 각 배포판의 패키지 매니저에 있습니다.)

##### Debian 계열

```sh
# 잘못된 디스크 사용 관련 로그는 무시해주세요
sudo apt install -fy ./rustdesk-<version>.deb
```

##### Red Hat 계열

```sh
sudo yum localinstall ./rustdesk-<version>.rpm
```

##### Arch Linux/Manjaro

```sh
sudo pacman -U ./rustdesk-<version>.pkg.tar.zst
```

##### openSUSE (≥ Leap 15.0)

```sh
sudo zypper install --allow-unsigned-rpm ./rustdesk-<version>-suse.rpm
```

##### Nix / NixOS (≥ 22.05)

`rustdesk`를 바로 실행할 수 있는 임시 셸에 진입하려면:

```sh
nix shell nixpkgs#rustdesk
```

현재 유저 프로파일에 설치하려면:

```sh
nix profile install nixpkgs#rustdesk
```

시스템 전체에 설치를 원하신다면 `configuration.nix` 파일을 수정 후 `nixos-rebuild switch --flake /etc/nixos` 커맨드를 실행해주세요:

```
  environment.systemPackages = with pkgs; [
    ...
    rustdesk
  ];
```

#### Android
GitHub를 통해 apk 파일을 설치해주세요. 더 많은 정보는 [Android page](https://rustdesk.com/docs/en/client/android/)를 참고해주세요.

#### iOS (iPhone, iPad)
[App Store](https://apps.apple.com/us/app/rustdesk-remote-desktop/id1581225015)에서 설치해주세요.

### 사용
RustDesk는 설치된 후(혹은 임시 실행파일로 실행된 후) 공용 서버로 연결할 것입니다. 아래에 (1) "준비, 자체 서버를 구축하면 더 빠른 속도로 사용할수 있습니다" 메시지가 표시되며, 좌상단에는 (2) ID, (3) 일회용 비밀번호가, 우측에는 (4) 상대 ID를 아는 경우 연결할 수 있도록 입력창이 표시됩니다.

![](/docs/en/client/images/client.png)

설정 메뉴는 ID 오른쪽의 (5) 메뉴 버튼 [ &#8942; ] 을 클릭해주세요.

설정 아래에서 다음 항목들을 찾을 수 있습니다:
- 일반 - 서비스 제어, 테마, 하드웨어 코덱, 오디오 입력 장치, 녹화, 언어
- 보안 - 다른 사람의 제어에 대한 권한, 비밀번호, ID 변경,고급 보안 설정
- 네트워크 - 자체 서버 설정, 프록시
- 디스플레이 - 원격 세션을 위한 디스플레이 설정 및 클립보드 동기화 등 기타 옵션
- 계정 - Pro Server와 함께 사용하여 API에 로그인
- 정보 - 소프트웨어 관련 정보 표시

### RustDesk 구성하기
RustDesk 구성에는 여러 방법이 존재합니다.

가장 쉬운 방법은 RustDesk Server Pro를 사용하는 것입니다. 이를 통해 암호화된 설정 문자열을 얻을 수 있으며, 이 문자열은 --config 옵션과 함께 사용하여 설정을 가져올 수 있습니다. 다음을 참고해주세요:
1. OS에 맞게 RustDesk 설치경로를 터미널로 열어주세요. 윈도우에서는 `C:\Program Files\RustDesk`, 리눅스에서는 `/usr/bin` 일 것입니다.
2. 커맨드를 실행해주세요: `rustdesk.exe --config 암호화-설정-문자열` e.g. `rustdesk.exe --config 9JSPSvJzNrBDasJjNSdXOVVBlERDlleoNWZzIHcOJiOikXZr8mcw5yazVGZ0NXdy5CdyciojI0N3boJye`.

직접 클라이언트를 설정할수도 있습니다. 아래를 참고해주세요:
1. 설정을 클릭해주세요.
2. 네트워크를 클릭해주세요.
3. 네트워크 설정 잠금 해제를 클릭해주세요.
4. ID, 릴레이, API(만약 pro server를 사용하시는 경우)와 키를 입력해주세요.

![](/docs/en/client/images/network-settings.png)

클라이언트를 수동으로 설정한 경우, 사용자 폴더에 있는 `RustDesk2.toml` 파일을 가져와 위의 예시와 유사하게 `--import-config` 옵션을 사용하여 설정을 불러올 수 있습니다.

### 커맨드라인 파라미터
- `--password` 를 통하여 영구 비밀번호를 설정할 수 있습니다.
- `--get-id` 를 통하여 ID를 확인할 수 있습니다.
- `--set-id` 를 통하여 ID를 설정할 수 있습니다. ID는 문자로 시작해야 합니다.
- `--silent-install` 를 통하여 Windows에서 RustDesk를 조용히(기타 조작 없이) 설치하는 데 사용할 수 있습니다.

더 많은 고급 파라미터는 [여기서](https://github.com/rustdesk/rustdesk/blob/bdc5cded221af9697eb29aa30babce75e987fcc9/src/core_main.rs#L242) 확인하실 수 있습니다.

{{% children depth="3" showhidden="true" %}}
