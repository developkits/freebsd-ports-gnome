# Created by: Andrej Zverev
# $FreeBSD$

PORTNAME=	lincity-ng
PORTVERSION=	2.0
PORTREVISION=	13
CATEGORIES=	games
MASTER_SITES=	BERLIOS

MAINTAINER=	mmokhi@FreeBSD.org
COMMENT=	Improved rich city simulation game for X

BUILD_DEPENDS=	jam:devel/jam
LIB_DEPENDS=	libphysfs.so:devel/physfs

USES=		pkgconfig tar:bzip2
USE_SDL=	sdl mixer image ttf gfx
USE_GL=		yes
USE_GNOME=	libxml2

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-libphysfs=${PREFIX} \
		--x-libraries=${LOCALBASE}/lib --x-includes=${LOCALBASE}/include
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-lpthread -L${LOCALBASE}/lib

PLIST_FILES=	bin/lincity-ng \
		share/applications/lincity-ng.desktop \
		share/pixmaps/lincity-ng.png
PORTDATA=	*
PORTDOCS=	*

OPTIONS_DEFINE=	DOCS

post-patch:
	@${REINPLACE_CMD} -e 's| -O| -I${LOCALBASE}/include&|g' \
		${WRKSRC}/Jamrules
do-build:
	@(cd ${BUILD_WRKSRC}; ${SETENV} ${MAKE_ENV} jam -j${MAKE_JOBS_NUMBER})

do-install:
	@(cd ${INSTALL_WRKSRC} && ${SETENV} ${MAKE_ENV} jam -sprefix=${STAGEDIR}${PREFIX} ${INSTALL_TARGET})

.include <bsd.port.mk>
