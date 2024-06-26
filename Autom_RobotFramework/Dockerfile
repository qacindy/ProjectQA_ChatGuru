# Use a imagem base do Windows Server
FROM mcr.microsoft.com/windows/servercore:ltsc2019

# Defina o diretório de trabalho
WORKDIR C:/Automation/ProjetoQA_ChatGuru/autom_robotframework

# Instale o Chocolatey
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Instale o Python
RUN choco install -y python3

# Instale o pip
RUN python -m pip install --upgrade pip

# Instale o Robot Framework e a SeleniumLibrary
RUN pip install robotframework robotframework-seleniumlibrary requests selenium

# Baixe e instale o ChromeDriver versão 126.0.6478.127
RUN $env:CHROMEDRIVER_VERSION = '126.0.6478.127'; \
    Invoke-WebRequest -Uri https://chromedriver.storage.googleapis.com/$env:CHROMEDRIVER_VERSION/chromedriver_win32.zip -OutFile chromedriver.zip; \
    Expand-Archive -Path chromedriver.zip -DestinationPath .; \
    Remove-Item -Force chromedriver.zip

# Copie os arquivos do projeto para o contêiner
COPY . .

# Defina o PATH para o ChromeDriver e o Python
ENV PATH="C:/Automation/ProjetoQA_ChatGuru/autom_robotframework;C:/Python39;C:/Python39/Scripts;${PATH}"

# Comando padrão para executar os testes
CMD ["robot", "--outputdir", "results/", "."]
