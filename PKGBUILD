# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Tobias Powalowski
#     <tpowa@archlinux.org>

_os="$(
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _compiler="clang"
  _libcompiler="llvm-libs"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
fi
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_git" ]]; then
  _git="true"
  # On Windows it builds
  # only from GNU tarball
  # release.
  if [[ "${_os}" == "Msys" ]]; then
    _git="false"
  fi
fi
if [[ ! -v "_ns" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _ns="gnu"
  elif [[ "${_git}" == "false" ]]; then
    _ns="themartiancompany"
  fi
  if [[ "${_os}" == "Msys" ]]; then
    _ns="gnu"
  fi
fi
if [[ ! -v "_release" ]]; then
  _release="false"
  if [[ "${_os}" == "Msys" ]]; then
    _release="true"
  fi
fi
if [[ ! -v "_git_service" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _git_service="${_ns}"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _git_service="github"
  fi
fi
if [[ "${_os}" == "Msys" ]]; then
  _git_service="gnu"
fi
if [[ ! -v "_tag_name" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    if [[ "${_release}" == "true" ]]; then
      _tag_name="tag"
    elif [[ "${_release}" == "false" ]]; then
      _tag_name="commit"
    fi
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _tag_name="commit"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    elif [[ "${_git_service}" == "gnu" ]]; then
      if [[ "${_release}" == "true" ]]; then
        _archive_format="tar.xz"
      elif [[ "${_release}" == "false" ]]; then
        _archive_format="tar.gz"
      fi
    fi
  fi
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
  if [[ "${_os}" == "Msys" ]]; then
    _docs="false"
  fi
fi
_py="python"
_proj=gnu
_pkg=findutils
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=4.11.0
_commit="66fc81d477f9e0e3dadeb80800c967d901f43ca7"
_gnulib_commit="a575239e473656fd0c055a228963bdb48bd0c2cb"
pkgrel=52
_pkgdesc=(
  "GNU utilities to locate files"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'aarch64'
  'armv8l'
  'armv7l'
  'armv6l'
  'arm'
  'i686'
  'mips'
  'pentium4'
  'powerpc'
  'x86_64'
)
license=(
  'GPL-3.0-or-later'
)
depends=(
  "${_libc}"
  "${_libcompiler}"
)
makedepends=(
  "${_compiler}"
  "gettext"
  "gperf"
  "${_py}"
  "wget"
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "texinfo"
  )
fi
# if [[ "${_os}" == "Android" ]]; then
#   makedepends+=(
#     "termux-fix-shebang"
#   )
# fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ ! -v "_tag" ]]; then
  if [[ "${_tag_name}" == "tag" ]]; then
    _tag="v${pkgver}"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _tag="${_commit}"
    _gnulib_tag="${_gnulib_commit}"
  fi
fi
_tarname="${_pkg}-${_tag}"
_github_sum="0aa6183ad71351039711e302646dfc46b5f7f8930414c88ddca9cb1319e41c4c"
_gnulib_github_sum="81f7839181261a17785d4d05a1b45d1e7e23c932ff093cb1100a8cbdf95b680c"
_gnu_release_sum='bfd19cb06cc71f3352d567e90284d8cdac02ac89774bbeadf0b533b0c11432fd'
if [[ "${_git}" == "true" ]]; then
  _tarfile="${_tarname}"
  _gnulib_tarname="gnulib"
  _gnulib_tarfile="${_gnulib_tarname}"
  _gnulib_sum="SKIP"
elif [[ "${_git}" == "false" ]]; then
  _tarfile="${_tarname}.${_archive_format}"
  _gnulib_tarname="gnulib-${_gnulib_tag}"
  _gnulib_tarfile="${_gnulib_tarname}.${_archive_format}"
  if [[ "${_ns}" == "themartiancompany" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _sum="${_github_sum}"
      _gnulib_sum="${_gnulib_github_sum}"
    fi
  elif [[ "${_ns}" == "gnu" ]]; then
    if [[ "${_release}" == "true" ]]; then
      _sum="${_gnu_release_sum}"
    fi
  fi
fi
url="https://www.${_proj}.org/software/${_pkg}"
if [[ "${_ns}" == "gnu" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _http="https://git.savannah.${_ns}.org/git"
  elif [[ "${_git}" == "true" ]]; then
    _http="https://ftp.${_ns}.org/pub/${_ns}"
  fi
fi
if [[ "${_git_service}" == "gnu" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _url="${_http}/${_pkg}.git"
    _gnulib_uri="${_http}/gnulib.git"
    _src="${_tarfile}::git+${_url}?signed#${_tag_name}=${_tag}"
    _gnulib_src="${_gnulib_tarfile}::git+${_gnulib_uri}"
  elif [[ "${_git}" == "false" ]]; then
    _url="${_http}/${_pkg}/${_tarname}.tar.xz"
    _src="${_tarfile}::${_uri}"
    _gnulib_src="${_gnulib_tarfile}::${_gnulib_uri}"
  fi
elif [[ "${_git_service}" == "github" ]]; then
  _http="https://${_git_service}.com"
  _url="${_http}/${_ns}/${_pkg}"
  _gnulib_url="${_http}/${_ns}/gnulib"
  if [[ "${_tag_name}" == "commit" ]]; then
    _uri="${_url}/archive/${_commit}.${_archive_format}"
    _gnulib_uri="${_gnulib_url}/archive/${_gnulib_commit}.${_archive_format}"
    _sum="${_github_sum}"
  else
    echo \
      "Not written." \
      1>&2
    exit \
      1
  fi
  _src="${_tarfile}::${_uri}"
  _gnulib_src="${_gnulib_tarfile}::${_gnulib_uri}"
fi
source=(
  "${_src}"
)
validpgpkeys=(
  # Bernhard Voelker
  #   <mail@bernhard-voelker.de>
  'A5189DB69C1164D33002936646502EF796917195'
  # James Youngman
  #   <james@youngman.org>
  '0CF4E8D871593224842832B888DD9E08C5DDACB9'
)
if [[ "${_git}" == "true" ]]; then
  b2sums=(
    '234e55a7eb5d9b882e45f9fb40446f765741130e4c3ebd01154344e48f0d3bcb6b36442d1c99c3574df239511959d542ec9b201fe269a1fd7b527edd058c54d5'
    'SKIP'
  )
elif [[ "${_git}" == "false" ]]; then
  sha256sums=(
    "${_sum}"
  )
fi
if [[ "${_release}" == "false" ]]; then
  source+=(
    "${_gnulib_src}"
  )
  sha256sums+=(
    "${_gnulib_sum}"
  )
fi

_android_fix_shebang() {
  local \
    _file="${1}" \
    _pattern \
    _repl
  _pattern="#! /bin/sh"
  _repl="#!/data/data/com.termux/files/usr/bin/env bash"
  sed \
    "s%${_pattern}%${_repl}%g" \
    -i \
    "${_file}"
}

prepare() {
  local \
    _bootstrap_opts=() \
    _gnulib_clone_path \
    _gnulib_srcdir_path \
    _os
  _gnulib_clone_path="${srcdir}/${_gnulib_tarname}"
  _gnulib_srcdir_path="${srcdir}/${_tarname}/gnulib"
  cd \
    "${_tarname}"
  if [[ "${_git}" == "true" ]]; then
    git \
      submodule \
        init
    git \
      config \
        "submodule.gnulib.url" \
        "${srcdir}/${_gnulib_tarname}"
    git \
      -c \
        "protocol.file.allow=always" \
      submodule \
        update
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_release}" == "false" ]]; then
      if [[ -e ".gitmodules" ]]; then
        rm \
          -v \
          "${PWD}/.gitmodules"
      fi
      if [[ -d "${_gnulib_srcdir_path}" ]]; then
        mv \
	  -v \
          "${_gnulib_clone_path}/"* \
          "${_gnulib_srcdir_path}"
      elif [[ ! -d "${_gnulib_srcdir_path}" ]]; then
        mv \
          -v \
          "${_gnulib_clone_path}" \
          "${_gnulib_srcdir_path}"
      fi
      # sed \
      #   -i
      #   "/prepare_GNULIB_SRCDIR$/d" \
      #   "${PWD}/bootstrap"
      _bootstrap_opts+=(
        --no-git
      )
      _os="$(
        uname \
          -o)"
      if [[ "${_os}" == "Android" ]]; then
        _android_fix_shebang \
          "${PWD}/bootstrap"
        _android_fix_shebang \
          "${_gnulib_srcdir_path}/gnulib-tool"
        _android_fix_shebang \
          "${_gnulib_srcdir_path}/gnulib-tool.py"
        # termux-fix-shebang \
        #   "/data/data/com.termux/files/usr/bin/fur";
      fi
      export \
        GNULIB_SRCDIR="${_gnulib_srcdir_path}"; \
      GNULIB_SRCDIR="${_gnulib_srcdir_path}" \
      "${PWD}/bootstrap" \
        "${_bootstrap_opts[@]}"
    elif [[ "${_release}" == "true" ]]; then
      autoreconf \
        -fi
    fi
  fi
}

build() {
  local \
    _configure_opts=()
  _configure_opts+=(
    --prefix="/usr"
  )
  cd \
    "${_tarname}"
  if [[ "${_os}" == "Msys" ]]; then
    if [[ "$CARCH" == "i686" ]]; then
      _configure_opts+=(
        --disable-year2038
      )
    fi
    _configure_opts+=(
      DEFAULT_ARG_SIZE="(32u*1024)"
      --disable-year2038
      --without-libiconv-prefix
      --without-libintl-prefix
    )
  fi
  # Don't build or install locate because we use mlocate,
  # which is a secure version of locate.
  sed \
    -e \
      '/^SUBDIRS/s/locate//' \
    -e \
      's/frcode locate updatedb//' \
    -i \
    "Makefile.in"
  ./configure \
    "${_configure_opts[@]}"
  # don't build locate, but the docs want a file in there.
  if [[ "${_docs}" == "true" ]]; then
    make \
      -C \
        "locate" \
      dblocation.texi
  fi
  make
}

check() {
  cd \
    "${_tarname}"
  make \
    check
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install
}
