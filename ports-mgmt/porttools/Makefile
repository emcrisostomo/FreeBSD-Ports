# Created by: Sergei Kolobov <sergei@kolobov.com>
# $FreeBSD$

PORTNAME=	porttools
PORTVERSION=	1.07
CATEGORIES=	ports-mgmt

MAINTAINER=	skreuzer@FreeBSD.org
COMMENT=	Tools for testing and submitting port updates and new ports

LICENSE=	BSD2CLAUSE

RUN_DEPENDS=	portlint:ports-mgmt/portlint \
		cdiff:textproc/cdiff \
		sudo:security/sudo \
		svn:devel/subversion

USE_GITHUB=	yes
GH_ACCOUNT=	skreuzer

# Make the version information of porttools itself
# available for inclusion in the PRs generated by it.
MAKE_ENV+=	DATADIR="${DATADIR}" DOCSDIR="${DOCSDIR}" PORTVERSION="${PORTVERSION}"

OPTIONS_DEFINE=		DOCS

DOCS_INSTALL_TARGET=	 install install-docs

.include <bsd.port.mk>
