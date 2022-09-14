---
title		: vscode ssh 접속 대상 서버가 폐쇄망일 경우 설정 방법
---

## 개요
vscode ssh로 서버 접속 시, 대상 서버의 /home/{username} 경로에 .vscode-server 디렉터리가 생성되고 각종 필요한 파일을 자동으로 인터넷에서 다운받게 된다.
따라서 해당 서버가 폐쇄망이면 파일 다운로드가 실패하게 되고, vscode ssh 접속도 되지 않는다.

## 해결 방법
1. 대상 서버의 다음 경로에서 commit id를 확인한다. /home/$USERNAME/.vscode-server/bin/**$COMMIT_ID**/
2. 인터넷 가능한 PC에서 다음 경로를 열어서 vscode-server.tar.gz 파일을 다운받는다.
https://update.code.visualstudio.com/commit:$COMMIT_ID/server-linux-x64/insider  (일단 x64인 경우만..)
3. 이 파일을 대상 서버에 업로드한다.
4. 압축 해제.
```sh
tar -xvzf vscode-server.tar.gz --strip-components 1 -C /home/$USERNAME/.vscode-server/bin/**$COMMIT_ID**/
```

## 링크
https://stackoverflow.com/questions/56718453/using-remote-ssh-in-vscode-on-a-target-machine-that-only-allows-inbound-ssh-co




