ARG UBUNTU20_04
FROM ohmymndy/ubuntu:$UBUNTU20_04
LABEL maintainer "Mandy Schoep <mandyschoep@gmail.com>"
SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]

USER root
RUN mkdir -p "$HOME"/{.wine,.wine64} \
	&& chown -R "$USER":"$USER" "$HOME"

RUN dpkg --add-architecture i386 \
	&& apt-get update \
	&& DEBIAN_FRONTEND=noninteractive \
	apt-get install -o APT::Immediate-Configure=false -y \
		wine \
		wine32 \
		wine64 \
		winetricks \
		winbind \
	&& apt-get install -y --no-install-recommends zenity \
	&& apt-get clean -y

RUN mkdir -p "/run/user/1000/$USER" \
	&& chown "$USER":"$USER" -R "/run/user/1000/$USER" \
	&& chmod 700 -R "/run/user/1000/$USER"


USER $USER

VOLUME $USER/.wine64
VOLUME $USER/.wine

ENTRYPOINT [ "wine" ]