# Maintener: sputnick <gilles DOT quenot AT gmail DOT com>
# Generator  : CPANPLUS::Dist::Arch 0.18
pkgname='perl-http-proxy'
pkgver='0.304'
pkgrel='1'
pkgdesc="HTTP proxy"
arch=('i686' 'x86_64')
license=('PerlArtistic' 'GPL')
makedepends=('perl-libwww' 'perl-test-simple')
url='http://search.cpan.org/dist/HTTP-Proxy'
source=("http://mirror.ibcp.fr/pub/CPAN/authors/id/B/BO/BOOK/HTTP-Proxy-${pkgver}.tar.gz" "HTTP-Proxy-0.304-Support-IPv6.patch" "HTTP-Proxy-0.304-Fix-Empty-Read.patch")
md5sums=('09ac64c5f67b7d8baff4ea135d74af48'
		 'd5f81bdb0fd2e24f0861718af8e8d20b'
		 '759d8a9bebb220a85426e46a9b34a79e')
_dist_dir="HTTP-Proxy-${pkgver}"

prepare() {
  cd "$_dist_dir"
  # Fix bug #120275. https://rt.cpan.org/Public/Bug/Display.html?id=120275
  patch -Np1 -i "${srcdir}/HTTP-Proxy-0.304-Support-IPv6.patch"
  # Fix bug. http://www.cpantesters.org/cpan/report/b7d0a086-d278-11e5-a2ee-9fa967b6c32e
  # https://github.com/book/HTTP-Proxy/issues/7
  patch -Np1 -i "${srcdir}/HTTP-Proxy-0.304-Fix-Empty-Read.patch"
}

build() {
  export PERL_MM_USE_DEFAULT=1 export PERL_AUTOINSTALL=--skipdeps
  { cd "$_dist_dir" &&
    /usr/bin/perl Makefile.PL INSTALLDIRS=vendor &&
    make &&
    make test
  } || return 1
}

package() {
    cd "$_dist_dir"
    find "$pkgdir" -name .packlist -o -name perllocal.pod -delete
    make DESTDIR="$pkgdir" install
}
