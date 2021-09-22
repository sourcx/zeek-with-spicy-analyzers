# zeek-with-spicy-analyzers

Info on:

- building zeek with spicy analyzers for Docker
- installing zeek with spicy analyzers on mac osx

## Docker

### Build

    docker-compose build

### Run

    docker run -ti zeek-with-spicy-analyzers:latest zeek -NN _Zeek::Spicy

### Update

This project uses the following releases:

- https://github.com/zeek/zeek/releases
- https://github.com/zeek/spicy/releases
- https://github.com/zeek/spicy-plugin/releases
- https://github.com/zeek/spicy-analyzers/releases

Dowload latest versions, update docker-compose.yml, remove old ones, build again.

## Mac OS

### Install

    brew install zeek
    brew tap zeek/zeek
    brew install spicy
    pip3 install zkg
    zkg install zeek/spicy-plugin
    export ZEEK_PLUGIN_PATH="$ZEEK_PLUGIN_PATH:$(zkg config state_dir)/clones/package/spicy-plugin"
    zkg install zeek/spicy-analyzers
    export ZEEK_PLUGIN_PATH="$ZEEK_PLUGIN_PATH:$(zkg config state_dir)/clones/package/spicy-analyzers"

### Run

    zeek -NN _Zeek::Spicy

### Update

    brew upgrade zeek
    brew upgrade spicy
    pip3 install zkg
    zkg upgrade zeek/spicy-plugin
    zkg upgrade zeek/spicy-analyzers
