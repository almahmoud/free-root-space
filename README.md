# Free Root Space on GitHub Linux Runners

## Background
This action removes pre-installed software on Linux GitHub runners to free up to over 70Gb of root space. This action was particularly made for the purpose of freeing up space for Docker build steps in workflows that do not otherwise require any pre-installed software. The list was created manually by examining the output of `sudo du --max-depth=4 / | sort -n` around March 2023.

This action is inspired by and can be used together with the [easimon/maximize-build-space action](https://github.com/easimon/maximize-build-space), which can notably create a directory with additional space by virtually mounting temp and swap space.

## How it works
In short, the action is equivalent to running `sudo rm -rf` on a list of directories, which is [exactly what it does](https://github.com/almahmoud/free-root-space/blob/main/action.yml#L184). The most significant advantage of using this action is inheriting changes as they come up and not have to manually do them across multiple workflows that might need extra root disk space (eg: different repos building Docker containers).

## Getting Started
You can use this action by adding it as a step in your workflow. The default configuration, which removes all identified pre-installed software, leaves a root disk with over 70Gb as of March 2023.

```yaml
    steps:
      - name: Free root space
        uses: almahmoud/free-root-space@main
        with:
          verbose: true
```

By default all identified directories are removed. You can keep software suites by setting their `remove-*` parameter to `false`.

For example, the below configuration will leave the .NET suite.

```yaml
    steps:
      - name: Free root space
        uses: almahmoud/free-root-space@main
        with:
          verbose: true
          remote-dotnet: false
```

The full list of options can be found in the action.yml file, or paste below:

```yaml
  verbose:
    description: 'Print a trace of commands (`set -x`)'
    required: false
    default: 'true'
  remove-dotnet:
    description: 'Removes /usr/share/dotnet /home/runner/.dotnet /home/runneradmin/.dotnet /etc/skel/.dotnet'
    required: false
    default: 'true'
  remove-android:
    description: 'Removes /usr/local/lib/android'
    required: false
    default: 'true'
  remove-haskell:
    description: 'Removes /opt/ghc /usr/local/.ghcup'
    required: false
    default: 'true'
  remove-hostedtoolcache:
    description: 'Removes /opt/hostedtoolcache/*'
    required: false
    default: 'true'
  remove-google-sdk:
    description: 'Removes /usr/lib/google-cloud-sdk'
    required: false
    default: 'true'
  remove-firefox:
    description: 'Removes /usr/lib/firefox'
    required: false
    default: 'true'
  remove-powershell:
    description: 'Removes /opt/microsoft/powershell'
    required: false
    default: 'true'
  remove-graalvm:
    description: 'Removes /usr/local/graalvm'
    required: false
    default: 'true'
  remove-rustup:
    description: 'Removes /etc/skel/.rustup /home/runner/.rustup /home/runneradmin/.rustup'
    required: false
    default: 'true'
  remove-llvm-12:
    description: 'Removes /usr/lib/llvm-12'
    required: false
    default: 'true'
  remove-llvm-13:
    description: 'Removes /usr/lib/llvm-13'
    required: false
    default: 'true'
  remove-llvm-14:
    description: 'Removes /usr/lib/llvm-14'
    required: false
    default: 'true'
  remove-julia:
    description: 'Removes /usr/local/julia*'
    required: false
    default: 'true'
  remove-microsoft:
    description: 'Removes /opt/microsoft'
    required: false
    default: 'true'
  remove-azure-cli:
    description: 'Removes /opt/az /usr/src/*-azure-* /usr/share/az_9.3.0'
    required: false
    default: 'true'
  remove-linuxbrew:
    description: 'Removes /home/linuxbrew'
    required: false
    default: 'true'
  remove-pipx:
    description: 'Removes /opt/pipx'
    required: false
    default: 'true'
  remove-google:
    description: 'Removes /opt/google'
    required: false
    default: 'true'
  remove-gcc:
    description: 'Removes /usr/lib/gcc'
    required: false
    default: 'true'
  remove-mono:
    description: 'Removes /usr/lib/mono'
    required: false
    default: 'true'
  remove-aws-cli:
    description: 'Removes /usr/local/aws-*'
    required: false
    default: 'true'
  remove-sql:
    description: 'Removes /var/lib/mysql /usr/local/sqlpackage /var/lib/postgresql /usr/lib/postgresql'
    required: false
    default: 'true'
  remove-gems:
    description: 'Removes /var/lib/gems'
    required: false
    default: 'true'
  remove-swift:
    description: 'Removes /usr/share/swift'
    required: false
    default: 'true'
  remove-miniconda:
    description: 'Removes /usr/share/miniconda'
    required: false
    default: 'true'
  remove-cargo:
    description: 'Removes /home/runner/.cargo /etc/skel/.cargo /home/runneradmin/.cargo'
    required: false
    default: 'true'
  remove-gradle:
    description: 'Removes /usr/share/gradle*'
    required: false
    default: 'true'
  remove-n:
    description: 'Removes /usr/local/n'
    required: false
    default: 'true'
  remove-cache:
    description: 'Removes /var/cache'
    required: false
    default: 'true'
  remove-sbt:
    description: 'Removes /usr/share/sbt /root/.sbt'
    required: false
    default: 'true'
  remove-mecab:
    description: 'Removes /var/lib/mecab'
    required: false
    default: 'true'
  remove-java:
    description: 'Removes /usr/share/java /usr/lib/jvm'
    required: false
    default: 'true'
  remove-fonts:
    description: 'Removes /usr/share/fonts'
    required: false
    default: 'true'
  remove-vim:
    description: 'Removes /usr/share/vim'
    required: false
    default: 'true'
  remove-icons:
    description: 'Removes /usr/share/icons'
    required: false
    default: 'true'
  remove-c++:
    description: 'Removes /usr/include/c++'
    required: false
    default: 'true'
  remove-mecab:
    description: 'Removes /usr/share/mecab'
    required: false
    default: 'true'
  remove-ri:
    description: 'Removes /usr/share/ri'
    required: false
    default: 'true'
  remove-R:
    description: 'Removes /usr/lib/R'
    required: false
    default: 'true'
  remove-kotlinc:
    description: 'Removes /usr/share/kotlinc'
    required: false
    default: 'true'
  remove-man-docs:
    description: 'Removes /usr/share/doc /usr/share/man'
    required: false
    default: 'true'
```
