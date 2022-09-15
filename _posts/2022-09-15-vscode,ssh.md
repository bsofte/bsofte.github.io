---
title		: vscode ssh 접속 설정
---
# 기본 설정

## PC 측

### 해당 extension: 
remote ssh, remote container

### oNE 환경
* VScode에서 직접 설치
* 메뉴 경로: VScode >> {좌측 창} Extention

### cNE 환경
* 해당 vsix 다운로드
https://marketplace.visualstudio.com/
* 설치
  + 메뉴 경로: VScode >> {좌측 창} Extention >> {우측 상단 '...'} Install from VSIX
  + 다운받은 vsic 설치


## 서버 측
### oNE 환경
ssh만 개방되어 있으면 된다. 그 외에 할 일 없다.
### cNE 환경
#### 개요
vscode ssh로 서버 접속 시, 대상 서버의 /home/$USERNAME 경로에 .vscode-server 디렉터리가 생성되고, ssh 접속에 필요한 각종 파일이 인터넷에서 자동 다운로드되어 이 경로에 저장된다. 이게 완료돼야 vscode ssh 접속이 완료된다.

따라서 해당 서버가 폐쇄망이면 파일 다운로드가 불가하므로, vscode ssh 접속정보를 맞게 설정해도 접속되지 않는다.

#### 링크
https://stackoverflow.com/questions/56718453/using-remote-ssh-in-vscode-on-a-target-machine-that-only-allows-inbound-ssh-co

#### 해결 방법
1. 대상 서버의 다음 경로에서 commit id를 확인한다.
/home/$USERNAME/.vscode-server/bin/**$COMMIT_ID**/
2. 인터넷 가능한 PC에서 다음 경로를 열어서 vscode-server.tar.gz 파일을 다운받는다.
https://update.code.visualstudio.com/commit:$COMMIT_ID/server-linux-x64/insider  (일단 x64인 경우만..)
3. 이 파일을 대상 서버에 업로드한다.
4. 압축 해제. (tar.gz 파일이므로 z 옵션을 꼭 줘야 한다 !!)
```sh
tar -xvzf vscode-server.tar.gz --strip-components 1 -C /home/$USERNAME/.vscode-server/bin/**$COMMIT_ID**/
```



# sudo 관련 vscode 확장 추가
* 파일 접근: ???
* 파일 저장: Save as Root in Remote
