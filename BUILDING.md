**Note:** In case you are looking for the pre-built releases see the [release page](https://github.com/k3s-io/k3s/releases/latest).

## Build k3s from source

Before getting started, bear in mind that this repository includes all of Kubernetes history, so consider shallow cloning with (`--depth 1`) to speed up the process.

```bash
git clone --depth 1 https://github.com/k3s-io/k3s.git
```

To build the full release binary, you may now run `make`, which will create `./dist/artifacts/k3s`.

To build the binaries using `make` without running linting (i.e.: if you have uncommitted changes):

```bash
SKIP_VALIDATE=true make
```

In case you make any changes to [go.mod](go.mod), you should run `go mod tidy` before running `make`.

### macOS considerations

The shell scripts in charge of the build process (the ones behind `make`) rely on GNU utils (i.e., `sed`), [which slightly differ on macOS](https://unix.stackexchange.com/a/79357). So, if you need to build k3s on a macOS environment, it is suggested to use the virtual machine defined on this repository's [Vagrantfile](Vagrantfile) to perform the tasks mentioned above.

To start the virtual machine, you will need [vagrant](https://www.vagrantup.com/) and [virtual box](https://www.virtualbox.org/) installed. Then prompt:

```bash
$ vagrant up
[... vm provisioning logs ...]
```

Once the virtual machine is provisioned, you should be able to ssh into it by doing `vagrant ssh` and perform any building task there:

```bash
$ vagrant ssh
[... ssh connection logs ..]
$ uname -a
Linux k3s-0-alpine312 5.11.0-41-generic
$ make
[... k3s build logs ...]
```

All the artifacts built within the VM will be synchronized with the directory where the `vagrant up` command was issued. For vagrant related commands please refer to [its cli documentation](https://www.vagrantup.com/docs/cli).
