
## Bağımlılıklar

 - Yazı düzenleyicisi, örn. [VS Code](https://code.visualstudio.com/).
 - [Docker](https://www.docker.com/) Ortamı kurma.
 - [Qemu](https://www.qemu.org/) Ortamı test etme.

## Kurulum

Ortam için İmaj kurun;
 - `docker build buildenv -t myos-buildenv`

## İnşa Etmek 

Ortamı İnşa Etmek İçin:
 - Linux or MacOS: `docker run --rm -it -v "$(pwd)":/root/env myos-buildenv`
 - Windows (CMD): `docker run --rm -it -v "%cd%":/root/env myos-buildenv`
 - Windows (PowerShell): `docker run --rm -it -v "${pwd}:/root/env" myos-buildenv`
 - Şunları kullanıyorsanız Linux komutu ile build edin; `WSL`, `msys2` or `git bash`

x86 Build
 - `make build-x86_64`

Çıkmak için; `exit`.

## Test Etme

Qemu ile Test Edebilirsiniz.[Qemu](https://www.qemu.org/): 

 - `qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso`

Komut başarısız olursa bunları deneyin:
 - Windows: [`qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso -L "C:\Program Files\qemu"`](https://stackoverflow.com/questions/66266448/qemu-could-not-load-pc-bios-bios-256k-bin)
 - Linux: [`qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso -L /usr/share/qemu/`](https://unix.stackexchange.com/questions/134893/cannot-start-kvm-vm-because-missing-bios)

## Temizleme

Build edilen ortamı kaldırın:
 - `docker rmi myos-buildenv -f`
