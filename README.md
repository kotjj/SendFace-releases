# SendFace


## Установка службы "SendFace"
При первом запуске команд установки NSSM автоматически распаковывается в папку рядом с SendFace.exe.
```
SendFace.exe --install
```

## Установка (PowerShell)

Скопируйте и выполните в PowerShell:
```powershell
if(!([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)){Start-Process powershell -Verb RunAs -ArgumentList '-NoProfile -ExecutionPolicy Bypass -Command $fd=\"$env:SystemDrive\SendFace\";$exe=\"$fd\SendFace.exe\";$url=\"https://github.com/kotjj/SendFace-releases/releases/latest/download/SendFace.exe\";if(!(Test-Path $fd)){New-Item -ItemType Directory -Path $fd -Force|Out-Null};$svc=Get-Service -Name \"SendFace\" -ErrorAction SilentlyContinue;if($svc -and $svc.Status -eq \"Running\"){Stop-Service -Name \"SendFace\" -Force};if(Get-Process -Name \"SendFace\" -ErrorAction SilentlyContinue){Stop-Process -Name \"SendFace\" -Force};Start-Sleep 2;for($i=0;$i-lt 5;$i++){try{if(Test-Path $exe){Remove-Item -Path $exe -Force -ErrorAction Stop};break}catch{Start-Sleep -Milliseconds 500}};Invoke-WebRequest -Uri $url -OutFile $exe -UseBasicParsing;Start-Process $exe -ArgumentList \"--install\"';exit};$fd="$env:SystemDrive\SendFace";$exe="$fd\SendFace.exe";$url="https://github.com/kotjj/SendFace-releases/releases/latest/download/SendFace.exe";if(!(Test-Path $fd)){New-Item -ItemType Directory -Path $fd -Force|Out-Null};$svc=Get-Service -Name "SendFace" -ErrorAction SilentlyContinue;if($svc -and $svc.Status -eq "Running"){Stop-Service -Name "SendFace" -Force};if(Get-Process -Name "SendFace" -ErrorAction SilentlyContinue){Stop-Process -Name "SendFace" -Force};Start-Sleep 2;for($i=0;$i-lt 5;$i++){try{if(Test-Path $exe){Remove-Item -Path $exe -Force -ErrorAction Stop};break}catch{Start-Sleep -Milliseconds 500}};Invoke-WebRequest -Uri $url -OutFile $exe -UseBasicParsing;Start-Process $exe -ArgumentList "--install"
```

Команда автоматически:
- Запрашивает права администратора
- Создаёт папку C:\SendFace
- Останавливает службу и процесс SendFace
- Скачивает последнюю версию
- Запускает установку

## Удаление службы "SendFace"
```
SendFace.exe --uninstall
```

## Простой запуск
Просто запустите SendFace.exe