# Created by: Shigeyuki FUKUSHIMA <shige@FreeBSD.org>
# $FreeBSD$

PORTNAME=	lynx
DISTVERSION=	${VERSION}.${MINOR_VERSION:S/.//}
CATEGORIES=	japanese www
MASTER_SITES=	http://invisible-mirror.net/archives/lynx/tarballs/
DISTNAME=	${PORTNAME}${VERSION}${MINOR_VERSION}

MAINTAINER=	CQG00620@nifty.ne.jp
COMMENT=	Console WWW client (browser) with multi-byte encoding support

LICENSE=	GPLv2

VERSION=	2.8.8
MINOR_VERSION=	rel.2

CONFLICTS=	lynx-2.* ja-lynx-2.8.9.*

WRKSRC=		${WRKDIR}/${PORTNAME}${VERSION:S/./-/g}
USES=		cpe ncurses shebangfix tar:bzip2
SHEBANG_FILES=	samples/mailto-form.pl
GNU_CONFIGURE=	yes
CONFIGURE_ARGS+=--with-screen=ncurses --with-zlib --libdir="${L_LIB}" \
		--enable-nsl-fork --enable-ipv6 \
		--enable-cjk --enable-internal-links \
		--with-bzlib
MAKE_ARGS=	helpdir=${L_HELP} docdir=${DOCSDIR}
MAKEFILE=	makefile
INSTALL_TARGET=	install-full
CPE_VERSION=	${PORTVERSION:R}
CPE_UPDATE=	${PORTVERSION:E:S/r/rel./}

L_LIB=		${PREFIX}/etc
L_HELP=		${PREFIX}/share/lynx_help

OPTIONS_DEFINE=	COLOR_STYLE DEFAULT_COLORS DOCS JAPANESE_UTF8
OPTIONS_DEFAULT=JAPANESE_UTF8
OPTIONS_SUB=	yes

COLOR_STYLE_DESC=		Optional color style support
COLOR_STYLE_CONFIGURE_ENABLE=	color-style

DEFAULT_COLORS_DESC=		Default-color background support (ncurses)
DEFAULT_COLORS_CONFIGURE_ENABLE=default-colors

JAPANESE_UTF8_DESC=		Experimental Japanese UTF-8 logic support
JAPANESE_UTF8_CONFIGURE_ON=	${ICONV_CONFIGURE_ARG}
JAPANESE_UTF8_CONFIGURE_ENABLE=	japanese-utf8
JAPANESE_UTF8_USES=		iconv

# Change "cd foo && $(MAKE_RECUR)" into "$(MAKE_RECUR) -C foo" to unbreak
# parallel builds
post-patch:
	@${REINPLACE_CMD} -E 's|cd (.+) && (\$$\(MAKE_RECUR\))|\2 -C \1|' \
		${WRKSRC}/${MAKEFILE}.in

.include <bsd.port.mk>
