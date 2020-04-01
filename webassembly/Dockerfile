FROM gitpod/workspace-full

RUN bash -cl "cargo install wasm-pack cargo-wasm cargo-generate \
    && curl \"https://wasmtime.dev/install.sh\" -sSf | bash"

RUN wget "https://github.com/CraneStation/wasi-sdk/releases/download/wasi-sdk-8/wasi-sdk_8.0_amd64.deb" \
    && sudo dpkg -i wasi-sdk_8.0_amd64.deb


RUN bash -cl "git clone \"https://github.com/emscripten-core/emsdk.git\" \
    && cd emsdk \
    && ./emsdk install latest \
    && ./emsdk activate latest \
    && source ./emsdk_env.sh"

RUN printf "\nsource /home/gitpod/emsdk/emsdk_env.sh\nclear\n" >> ~/.bashrc

WORKDIR /opt

RUN sudo git clone "https://github.com/WebAssembly/binaryen.git" \
    && cd binaryen \
    && sudo env "PATH=$PATH" cmake . && make \
    && cd .. \
    && sudo rm -rf binaryen

ENV PATH="/opt/wasi-sdk/bin:/opt/binaryen/bin:$PATH"
