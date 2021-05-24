![banner](https://user-images.githubusercontent.com/107757/119279427-9150eb80-bbe0-11eb-88d3-9e54e03b8020.jpg)

# cloutreactor (alpha)

cloutreactor is an *experimental* BitClout miner and PPLNS pool.

- This is *alpha* software. You are an alpha tester. The miner may crash, shares may not be counted correctly. Please create an issue if you are having trouble and it will be addressed ASAP.
- Work is tracked on the pool server: balance computation is experimental and will be confirmed before first payouts are issued manually.
- Please watch the repo: new versions may come at any time.

### Pool
- Pool statistics, miner management, and payouts will soon be enabled on cloutreactor.com via BitClout Identity.
- 10% of payouts will be invested into [@cloutreactor](https://bitclout.com/u/cloutreactor) on BitClout (50% FR)

### Miner
- NVIDIA CUDA 11 is currently supported
  - OpenCL support coming soon
  - GTX 10XX (Pascal) series and higher are supported

## Running the Miner

### Linux

#### Running via Docker (recommended)
  1) Install Docker
      - For Ubuntu: https://docs.docker.com/engine/install/ubuntu/

  2) Install the [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) for your platform

  3) At a command prompt, run cloutreactor with all GPUs:

  ```Shell
# Run in-process:
  sudo docker run --rm --name cloutreactor --gpus all --runtime nvidia cloutreactor/cuda:v0.0.1 --public-key="BC1YLhL2beeonivCELUydf1Dt4LFPxuNbSrz5GRmzKxdCxDDutiuFp9"

# Or as a daemon:
  sudo docker run --rm -d --name cloutreactor --gpus all --runtime nvidia cloutreactor/cuda:v0.0.1 --public-key="BC1YLhL2beeonivCELUydf1Dt4LFPxuNbSrz5GRmzKxdCxDDutiuFp9"
  sudo docker logs -f cloutreactor
  ```

#### Running compiled binaries

1) Install [CUDA 11.2](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) for your platform

2) Download the [latest release](https://github.com/cloutreactor/release/releases)

3) At a command prompt, run the server binary:

```Shell
./cloutreactor-linux-amd64 --public-key="BC1YLhL2beeonivCELUydf1Dt4LFPxuNbSrz5GRmzKxdCxDDutiuFp9"
```


### Windows

#### Running compiled binaries (recommended)

1) Install [CUDA 11.2](https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html) for your platform

2) Download the [latest release .exe file](https://github.com/cloutreactor/release/releases)

3) At a command prompt, run the server binary:

```Shell
./cloutreactor-windows-amd64.exe --public-key="BC1YLhL2beeonivCELUydf1Dt4LFPxuNbSrz5GRmzKxdCxDDutiuFp9"
```

**NOTE:** Multi-GPU support in the compiled Windows binary is currently not working. Use the '-d' flag and launch one instance of cloutreactor.exe per GPU.

#### Running via WSL2/Docker

1) Upgrade Windows 10 to [Insider `Dev` Channel](https://insider.windows.com/en-us/getting-started)

2) Install [WSL2]( https://docs.microsoft.com/en-us/windows/wsl/install-win10#simplified-installation-for-windows-insiders) and [Ubuntu 18.04](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)

3) Install [Docker Desktop with WSL2 Support](https://docs.docker.com/docker-for-windows/install/)

4) Install [NVIDIA WSL Preview Drivers](https://developer.nvidia.com/cuda/wsl/download)

5) Install [CUDA Toolkit for WSL](https://docs.nvidia.com/cuda/wsl-user-guide/index.html#running-cuda)

6) At a WSL command prompt, run cloutreactor with all GPUs:

```Shell
sudo docker run --rm -t -i --gpus all --runtime nvidia cloutreactor/cuda:v0.0.1 --public-key="BC1YLhL2beeonivCELUydf1Dt4LFPxuNbSrz5GRmzKxdCxDDutiuFp9"
```

## Coming Soon

- cloutreactor.com
  - BitClout Identity support
  - Payouts
  - Miner management
- OpenCL
- Prometheus metrics

## FAQ

- What is a share?
  - The cloutreactor pool divides work up between miners. Miners work on reduced-difficulty versions of a given block and are rewarded proportionately based on the number of hashes they compute. The absolute number of shares will vary widely between machines, GPUs, etc. Rewards are assigned based on total hash count, not total share count.
