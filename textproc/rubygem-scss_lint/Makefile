# $FreeBSD$

PORTNAME=	scss_lint
PORTVERSION=	0.55.0
CATEGORIES=	textproc rubygems
MASTER_SITES=	RG

MAINTAINER=	ruby@FreeBSD.org
COMMENT=	SCSS linter

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/MIT-LICENSE

RUN_DEPENDS=	rubygem-rake>=0.9:devel/rubygem-rake \
		rubygem-sass34>=0:textproc/rubygem-sass34

NO_ARCH=	yes
USE_RUBY=	yes
USES=		gem

PLIST_FILES=	bin/scss-lint

.include <bsd.port.mk>
