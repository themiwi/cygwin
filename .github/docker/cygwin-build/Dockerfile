FROM mcr.microsoft.com/windows/nanoserver:10.0.17763.1397-amd64

LABEL name="Cygwin Build Container"
LABEL description="This container is a Windows container for building Cygwin packages."
LABEL maintainer="Michael Wild <michael.andreas.wild@gmail.com>"

# Install chocolatey
RUN powershell.exe \
  -NoProfile -InputFormat None -ExecutionPolicy Bypass \
  -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" \
  && SETX PATH "%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

RUN choco install -y cygwin mingw \
  && RD /S /Q %localappdata%\NuGet

RUN curl https://raw.githubusercontent.com/transcode-open/apt-cyg/master/apt-cyg -o apt-cyg \
  && /tools/cygwin/bin/install apt-cyg /bin \
  && del apt-cyg

WORKDIR "/tools/cygwin/bin"
SHELL ["bash.exe", "--login", "-c"]

RUN apt-cyg install \
  autoconf automake libtool make pkg-config \
  cygport \
  gettext-devel \
  git \
  libevent-devel \
  libffi-devel \
  libncurses-devel \
  libsodium-devel \
  python python-pip python-devel python-wheel python-six python-cffi python-pycparser python-test \
  python3 python3-pip python3-devel python3-wheel python3-six python3-cffi python3-pycparser python3-test \
  python36 python36-pip python36-devel python36-wheel python36-six python36-cffi python36-pycparser python36-test \
  python37 python37-pip python37-devel python37-wheel python37-six python37-cffi python37-pycparser python37-test \
  python38 python38-pip python38-devel python38-wheel python38-six python38-cffi python38-pycparser python38-test \
  python-pip-wheel python-setuptools-wheel \
  python-cryptography \
  wget

CMD ["bash.exe", "--login", "-i"]

# vim: expandtab shiftwidth=2 tabstop=2 smartindent autoindent :
