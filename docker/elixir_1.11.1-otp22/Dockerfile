FROM erlang:22

# elixir expects utf8.
ENV ELIXIR_VERSION="v1.11.1" \
	LANG=C.UTF-8

ARG UID=1000

RUN useradd -d /home/iex_user -ms /bin/bash -g root -G sudo -u $UID iex_user

RUN set -xe \
	&& ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/${ELIXIR_VERSION}.tar.gz" \
	&& ELIXIR_DOWNLOAD_SHA256="724774eb685b476a42c838ac8247787439913667fe023d2f1ed9c933d08dc57c" \
	&& curl -fSL -o elixir-src.tar.gz $ELIXIR_DOWNLOAD_URL \
	&& echo "$ELIXIR_DOWNLOAD_SHA256  elixir-src.tar.gz" | sha256sum -c - \
	&& mkdir -p /usr/local/src/elixir \
	&& tar -xzC /usr/local/src/elixir --strip-components=1 -f elixir-src.tar.gz \
	&& rm elixir-src.tar.gz \
	&& cd /usr/local/src/elixir \
	&& make install clean \
	&& mix local.hex --force \
   	&& mix local.rebar --force
	
CMD ["/bin/sleep", "3600"]

