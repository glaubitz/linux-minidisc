Fedora-specific Build/Setup Instructions
========================================

Install build-dependencies:

Prior to Fedora 33

    sudo dnf install \
        qt5-devel libgcrypt-devel libmad-devel \
        libid3tag-devel glib-devel taglib-devel

Fedora 33+

    sudo dnf install \
        qt5-qtbase-devel libgcrypt-devel libmad-devel \
        libid3tag-devel glib-devel taglib-devel

Symlink translation tools:

    sudo ln -s /usr/bin/lupdate-qt5 /usr/bin/lupdate
    sudo ln -s /usr/bin/lrelease-qt5 /usr/bin/lrelease

Build everything:

    qmake-qt5
    make

Create plugdev group and copy udev rules:

    sudo groupadd plugdev
    # ... add your user to the plugdev group ...
    sudo cp netmd/etc/netmd.rules /etc/udev/rules.d/
    sudo systemctl restart systemd-udevd.service
    # ... re-plug the NetMD and/or reboot ...

