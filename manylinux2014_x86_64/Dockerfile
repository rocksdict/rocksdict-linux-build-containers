FROM quay.io/pypa/manylinux2014_x86_64

WORKDIR /root

RUN git clone --depth 1 --branch llvmorg-20.1.5 https://github.com/llvm/llvm-project.git

WORKDIR /root/llvm-project
RUN cmake -S llvm -B build \
    -G "Unix Makefiles" \
    -DLLVM_ENABLE_PROJECTS="clang;lld" \
    -DCMAKE_BUILD_TYPE=Release \
    -DLLVM_PARALLEL_COMPILE_JOBS=4 \
    -DLLVM_PARALLEL_LINK_JOBS=4
RUN cmake --build build --parallel 4 --config Release
RUN cmake --install build --config Release --prefix /usr/local

WORKDIR /root
RUN rm -rf llvm-project

# add these env in github action, so we do not need to set them here.

# ENV LIBCLANG_PATH=/usr/local/lib
# ENV CC=/usr/local/bin/clang
# ENV CXX=/usr/local/bin/clang++
# ENV AR=/usr/local/bin/llvm-ar
# ENV CFLAGS="-flto=thin -O3"
# ENV CXXFLAGS="-flto=thin -O3"
# ENV RUSTFLAGS="-Clinker-plugin-lto -Clinker=/usr/local/bin/clang -Clink-arg=-fuse-ld=/usr/local/bin/ld.lld"
