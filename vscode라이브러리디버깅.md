### vscode Breakpoint in file excluded by filters.

![image](https://github.com/moon0I980616I/errorlog/assets/144082197/9f9ca27f-3bfc-4f34-b26c-68a01ec31cd4)


https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc

vscdoe에서 작업 영역이 많아서 감시자 핸들이 부족하다고 했다.

링크 가이드대로 진행하던 중 `sysctl -p` 입력 시 

`sysctl: setting key "fs.inotify.max_user_watches", ignoring: Read-only file system`

![image](https://github.com/moon0I980616I/errorlog/assets/144082197/f0d2b6b1-2b70-4a18-8230-018d1a52c89a)


이 오류가 계속 뜨고 변경이 되지 않았다.

그래서 검색해봤더니 https://tttsss77.tistory.com/153 —privileged 모드로 도커를 실행하면 시스템 주요 자원에 접근할 수 있다고 해서 변경할 수 있었다.

![image](https://github.com/moon0I980616I/errorlog/assets/144082197/15df7a5e-fe82-47b5-ac28-a53123021544)
