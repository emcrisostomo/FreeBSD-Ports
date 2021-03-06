# Created by: DarwinSurvivor <darwinsurvivor@gmail.com>
# $FreeBSD$

PORTNAME=	notmuch
PORTVERSION=	0.25.1
CATEGORIES=	mail
MASTER_SITES=	http://notmuchmail.org/releases/

MAINTAINER=	mp39590@gmail.com
COMMENT=	Thread-based email index, search, and tagging application

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/COPYING-GPL-3

BUILD_DEPENDS=	c++filt:devel/binutils
LIB_DEPENDS=	libgmime-2.6.so:mail/gmime26 \
		libxapian.so:databases/xapian-core \
		libtalloc.so:devel/talloc
TEST_DEPENDS=	bash:shells/bash \
		emacs:editors/emacs-nox11 \
		dtach:misc/dtach \
		gdate:sysutils/coreutils \
		gbase64:sysutils/coreutils \
		gsed:textproc/gsed \
		gsha256sum:sysutils/coreutils \
		gpg:security/gnupg \
		gwc:sysutils/coreutils \
		${LOCALBASE}/bin/gdb:devel/gdb

BROKEN_powerpc64=	Does not build

HAS_CONFIGURE=	yes
USES=		gmake pkgconfig python:build,test
USE_GNOME=	glib20
CONFIGURE_ARGS=	--prefix=${PREFIX} --mandir=${MANPREFIX}/man
USE_LDCONFIG=	yes

MAKE_ENV+=	PYTHONCMD=${PYTHON_CMD}

TEST_ENV+=	NOTMUCH_SKIP_TESTS="address basic count crypto db-features \
		database-modified dump-restore emacs emacs-large-search-buffer \
		from-guessing insert json lib-error new parse-time-string \
		python search search-output sexp smime symbol-hiding tagging \
		thread-order thread-search" \
		V=1 \
		TEST_CFLAGS="-g -O0 -I${LOCALBASE}/include -L${LOCALBASE}/lib" \
		BSD_GDB=${LOCALBASE}/bin/gdb

TEST_TARGET=	test

OPTIONS_DEFINE=	BASH DESKTOP DOXYGEN EMACS MANPAGES MUTT RUBY ZSH
DESKTOP_DESC=	Install desktop file
EMACS_DESC=	Install EMACS lisp files (requires emacs)
MUTT_DESC=	Install notmuch-mutt script
OPTIONS_SUB=	yes

BASH_BUILD_DEPENDS=	bash-completion>=1.90:shells/bash-completion
BASH_RUN_DEPENDS=	${BASH_BUILD_DEPENDS}
BASH_CONFIGURE_WITH=	bash-completion
DESKTOP_CONFIGURE_WITH=	desktop
DESKTOP_USES=		desktop-file-utils
DOXYGEN_CONFIGURE_WITH=	api-docs
DOXYGEN_BUILD_DEPENDS=	doxygen:devel/doxygen
EMACS_CONFIGURE_WITH=	emacs
EMACS_CONFIGURE_ON=	--emacslispdir=${PREFIX}/${EMACS_SITE_LISPDIR} \
			--emacsetcdir=${PREFIX}/${EMACS_SITE_LISPDIR}
EMACS_USE=	EMACS=yes
MANPAGES_BUILD_DEPENDS=	sphinx-build:textproc/py-sphinx
MUTT_RUN_DEPENDS=	p5-Term-ReadLine-Gnu>0:devel/p5-Term-ReadLine-Gnu \
			p5-Mail-Tools>0:mail/p5-Mail-Tools \
			p5-Mail-Box>0:mail/p5-Mail-Box \
			p5-String-ShellQuote>0:textproc/p5-String-ShellQuote
MUTT_USES=	perl5
RUBY_USE=	RUBY=yes
ZSH_CONFIGURE_WITH=	zsh-completion

do-build-MUTT-on:
	${MAKE_CMD} -C ${WRKSRC}/contrib/notmuch-mutt all
	${GZIP_CMD} ${WRKSRC}/contrib/notmuch-mutt/notmuch-mutt.1

do-install-MUTT-on:
	${INSTALL_SCRIPT} ${WRKSRC}/contrib/notmuch-mutt/notmuch-mutt ${STAGEDIR}${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/contrib/notmuch-mutt/notmuch-mutt.1.gz ${STAGEDIR}${MANPREFIX}/man/man1

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/notmuch
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libnotmuch.so.5.0.0

.include <bsd.port.mk>
