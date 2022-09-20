# Ubuntu 22.04 LTS 설치 (WSL 2)

> 본 글에서는 되도록 명령줄만을 사용하여 간단하게 설치하는 과정을 소개합니다.

<span style="line-height: 80px;"></span>

## <span style="background: green;">WSL 2 (Windows Subsystem For Linux 2) 소개</span>

- 윈도우 환경에서 우분투 등 리눅스 환경을 사용할 경우 유용합니다.
- 윈도우에서 VMware 등 가상머신을 사용하는 경우와 비교해 다음과 같은 점이 편리했습니다.
	- CMD, Power Shell에서 바로 리눅스 환경에 접근이 가능합니다.
	- 가상머신을 사용하는 경우 보통 자원(메모리, 디스크 용량, CPU 코어 등)을 별도로 할당해주어야 하지만, WSL은 이를 별도로 할당하지 않아 자원 낭비가 적습니다.

<span style="line-height: 80px;"></span>

## <span style="background: green;">설치 전 확인 사항</span>

>WSL 2 requires **Windows 10 version 1903 or higher**, with **Build 18362 or higher**, for **x64 systems**, and **Version 2004 or higher**, with **Build 19041 or higher**, for **ARM64 systems**.
>- 출처 : [Windows Subsystem for Linux - Wikipedia](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
- 버전이 낮은 경우 윈도우 업데이트를 먼저 진행해주세요.

<span style="line-height: 80px;"></span>

## <span style="background: green;">설치</span>

### 1. PowerShell을 관리자 권한으로 실행합니다.

<div style="text-align: center;"><img style="max-width: 100%;" src="https://github.com/kwangwan/markdownFiles/blob/main/blog/image/PowerShell%20%EA%B4%80%EB%A6%AC%EC%9E%90%EA%B6%8C%ED%95%9C%20%EC%8B%A4%ED%96%89.png?raw=true"></div>

<span style="line-height: 80px;"></span>

### 2. 아래의 커맨드를 입력합니다.

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
> Windows의 "Linux용 Windows 하위 시스템" 기능을 켜는 커맨드입니다.


```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
> Windows의 "가상 머신 플랫폼" 기능을 켜는 커맨드입니다.

<div style="text-align: center;"><img style="max-width: 100%;" src="https://github.com/kwangwan/markdownFiles/blob/main/blog/image/PowerShell%20WSL%20%EA%B8%B0%EB%8A%A5%20%EC%BC%9C%EA%B8%B0.png?raw=true"></div>

<span style="line-height: 80px;"></span>

### 3. 윈도우를 다시 시작합니다.

<div style="text-align: center;"><img style="max-width: 100%;" src="https://github.com/kwangwan/markdownFiles/blob/main/blog/image/%EC%9C%88%EB%8F%84%EC%9A%B0%20%EB%8B%A4%EC%8B%9C%20%EC%8B%9C%EC%9E%91.png?raw=true"></div>

<span style="line-height: 80px;"></span>

### 4. 아래 링크에서 Linux 커널 업데이트 패키지를 다운로드하여 설치합니다.

[https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
- 위 링크는 [learn.microsoft.com의 "이전 버전 WSL의 수동 설치 단계"](https://learn.microsoft.com/ko-kr/windows/wsl/install-manual) 문서에서 가져왔습니다.

<span style="line-height: 80px;"></span>

### 5. PowerShell을 다시 관리자 권한으로 실행하여 다음 커맨드를 입력합니다.

```powershell
wsl --set-default-version 2
```
>WSL의 기본 버전을 WSL 2로 지정하는 커맨드입니다.

<div style="text-align: center;"><img style="max-width: 100%;" src="https://github.com/kwangwan/markdownFiles/blob/main/blog/image/PowerShell%20WSL2%20%EC%84%A4%EC%A0%95.png?raw=true"></div>

<span style="line-height: 80px;"></span>

### 6. 아래 커맨드를 입력하여 Ubuntu 22.04 LTS를 다운로드하여 설치합니다.

```powershell
Invoke-WebRequest -Uri https://aka.ms/wslubuntu2204 -OutFile Ubuntu.appx -UseBasicParsing
```
> Ubuntu 22.04 LTS를 다운로드하는 커맨드입니다. (예상 소요 시간: 45분)

```powershell
Add-AppxPackage .\Ubuntu.appx
```
> Ubuntu 22.04 LTS를 설치하는 커맨드입니다.

```powershell
rm .\Ubuntu.appx
```
> 설치가 완료된 Ubuntu.appx 파일을 삭제합니다.

<div style="text-align: center;"><img style="max-width: 100%;" src="https://github.com/kwangwan/markdownFiles/blob/main/blog/image/PowerShell%20Ubuntu%20%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%20%EB%B0%8F%20%EC%84%A4%EC%B9%98.png?raw=true"></div>

<span style="line-height: 80px;"></span>

## <span style="background: green;">참고 자료</span>

- [https://learn.microsoft.com/ko-kr/windows/wsl/install-manual](https://learn.microsoft.com/ko-kr/windows/wsl/install-manual)
- [https://learn.microsoft.com/ko-kr/windows/wsl/install](https://learn.microsoft.com/ko-kr/windows/wsl/install)