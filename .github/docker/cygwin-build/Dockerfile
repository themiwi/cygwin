FROM mcr.microsoft.com/windows/servercore:10.0.17763.1397-amd64

LABEL name="Cygwin Build Container"
LABEL description="This container is a Windows container for building Cygwin packages."
LABEL maintainer="Michael Wild <michael.andreas.wild@gmail.com>"

ENV CYGWIN winsymlinks:lnk

ADD setup-x86_64.exe /tmp/setup-x86_64.exe

RUN powershell -Command " \
    cd /tmp; \
    $cygpackages = @( \
      'default' \
    ); \
    ./setup-x86_64.exe -B -W -n -q -R C:/Cygwin64 -s http://mirrors.kernel.org/sourceware/cygwin/ \
      -P ($cygpackages -join ','); \
    Wait-Process -Name setup-x86_64; \
    cd ..; \
    rm -r tmp; \
    "

WORKDIR "C:/Cygwin64/bin"
CMD ["bash.exe", "--login", "-i"]

# vim: expandtab shiftwidth=2 tabstop=2 smartindent autoindent :
