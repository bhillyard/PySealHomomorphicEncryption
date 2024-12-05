# PySealHomomorphicEncryption
Implementing homomorphic encryption on credit score data

"I referred to the installation guidelines provided in the official SEAL-Python GitHub repository to set up and configure PySEAL. The instructions in the README were instrumental in ensuring a successful installation and integration of the library." (https://github.com/Huelse/SEAL-Python?tab=readme-ov-file#build)

# Optional
sudo apt-get install git build-essential cmake python3 python3-dev python3-pip

# Get the repository or download from the releases
git clone https://github.com/Huelse/SEAL-Python.git
cd SEAL-Python

# Install dependencies
pip3 install numpy pybind11

# Init the SEAL and pybind11
git submodule update --init --recursive
# Get the newest repositories (dev only)
# git submodule update --remote

# Build the SEAL lib without the msgsl zlib and zstandard compression
cd SEAL
cmake -S . -B build -DSEAL_USE_MSGSL=OFF -DSEAL_USE_ZLIB=OFF -DSEAL_USE_ZSTD=OFF
cmake --build build
cd ..

# Run the setup.py, the dynamic library will be generated in the current directory
python3 setup.py build_ext -i

# Test
cp seal.*.so examples
cd examples
python3 4_bgv_basics.py

# When the test successfully runs you should be able to run the creditScoreHE.ipynb file