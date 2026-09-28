cd 'G:\APP Local\Duckstation-Mikagura-test\duckstation'

$version = (Get-Content .\dep\PREBUILT-VERSION).Trim()
curl.exe -fL -o deps-windows-x64.7z "https://github.com/duckstation/dependencies/releases/download/$version/deps-windows-qt-installer-x64.7z"
& 'C:\Program Files\7-Zip\7z.exe' x .\deps-windows-x64.7z '-o.\dep\prebuilt'

& 'G:\Microsoft Visual Studio\2026\MSBuild\Current\Bin\MSBuild.exe' `
  .\duckstation.sln /m /t:Build /p:Configuration=Release /p:Platform=x64

  <PreprocessorDefinitions Condition="$(Configuration.Contains(Debug)) And !$(Configuration.Contains(Clang))">QT_NO_DEPRECATED_WARNINGS;%(PreprocessorDefinitions)</PreprocessorDefinitions>

  <PreprocessorDefinitions Condition="!$(Configuration.Contains(Clang))">QT_NO_DEPRECATED_WARNINGS;%(PreprocessorDefinitions)</PreprocessorDefinitions>

  cd 'G:\APP Local\Duckstation-Mikagura-test\duckstation'

& 'G:\Microsoft Visual Studio\2026\MSBuild\Current\Bin\MSBuild.exe' `
  .\duckstation.sln /m /t:Build /p:Configuration=Release /p:Platform=x64