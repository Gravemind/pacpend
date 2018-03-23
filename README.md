## pacpend

`pacman -Qu` output, but more customizable. Inspired by `VerbosePkgLists`, `yaourt -Qu`, and `pacaur -Qu`.

Uses `checkupdates` [safe temporary database](https://wiki.archlinux.org/index.php/System_maintenance#Partial_upgrades_are_unsupported) by default.

Can sort, group, highlights explicitly installed packages, query AUR database...

See `pacpend -h` for more.

## Usage

Usage with `checkupdates` for safe update checking:

* Check updates:
  ``` shell
  $> checkupdates > /dev/null && pacpend
  ```

* Check and download updates as user:

  * Setup once as root to give "download rights"
    (should be mostly safe for a personal computer: pacman checksums/verfies packages before install)
    ``` shell
    $> sudo chmod a+w /var/cache/pacman/pkg
    ```
  * Now, as a user you can safely **check and download updates**:
    ``` shell
    $> checkupdates > /dev/null; pacpend; echo ":: Downloading only:"; \
     fakeroot -- pacman --noconfirm -Suwb "${TMPDIR:-/tmp}/checkup-db-${USER}/"
    ```

## Dependencies

* archlinux
* python3
* [pyalpm](https://www.archlinux.org/packages/extra/x86_64/pyalpm/): Libalpm (pacman) bindings for Python 3
