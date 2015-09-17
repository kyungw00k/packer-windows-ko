# packer-windows-ko

## Introduction
한글판 윈도우를 위한 Packer Template 입니다.

## Windows Versions
지원하는 윈도우 버전은 다음과 같습니다.

 * Windows 10 Pro Korean x64
 * Windows 10 Pro KN Korean x64

## Product Keys
`Autounattend.xml` 파일에서 사용한 Produck Key는 http://technet.microsoft.com/en-us/library/jj612867.aspx 페이지를 참고했습니다.

## Windows Updates
이미지 생성 시간을 고려해 업데이트는 하지 않도록 했습니다. 하지만 필요하면 `Autounattend.xml` 파일을 아래와 같이 바꿔주면 되겠습니다.

```xml
<!-- WITHOUT WINDOWS UPDATES -->
<!--
<SynchronousCommand wcm:action="add">
    <CommandLine>cmd.exe /c C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -File a:\openssh.ps1 -AutoStart</CommandLine>
    <Description>Install OpenSSH</Description>
    <Order>99</Order>
    <RequiresUserInput>true</RequiresUserInput>
</SynchronousCommand>
-->
<!-- END WITHOUT WINDOWS UPDATES -->
<!-- WITH WINDOWS UPDATES -->
<SynchronousCommand wcm:action="add">
    <CommandLine>cmd.exe /c a:\microsoft-updates.bat</CommandLine>
    <Order>98</Order>
    <Description>Enable Microsoft Updates</Description>
</SynchronousCommand>
<SynchronousCommand wcm:action="add">
    <CommandLine>cmd.exe /c C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -File a:\openssh.ps1</CommandLine>
    <Description>Install OpenSSH</Description>
    <Order>99</Order>
    <RequiresUserInput>true</RequiresUserInput>
</SynchronousCommand>
<SynchronousCommand wcm:action="add">
    <CommandLine>cmd.exe /c C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -File a:\win-updates.ps1</CommandLine>
    <Description>Install Windows Updates</Description>
    <Order>100</Order>
    <RequiresUserInput>true</RequiresUserInput>
</SynchronousCommand>
<!-- END WITH WINDOWS UPDATES -->
```

## Acknowledgements
참고로, 스크립트와 템플릿은 아래 두 Repository에서 가져왔습니다.

* https://github.com/joefitzgerald/packer-windows
* https://github.com/boxcutter/windows

## Use Pre-built Image
* [Windows 10 Pro K x64](https://atlas.hashicorp.com/kyungw00k/boxes/windows-10-pro-k-x64)
* [Windows 10 Pro KN x64](https://atlas.hashicorp.com/kyungw00k/boxes/windows-10-pro-kn-x64)

## Contributing
Pull request 해주시면 좋죠.
