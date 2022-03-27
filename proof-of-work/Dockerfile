FROM ethereum/client-go:v1.10.16

ARG INITIAL_ACCOUNT_PASSWORD

# Bootstrap from our own genesis block
COPY genesis-block.json /tmp
RUN geth init /tmp/genesis-block.json

# Remove the nodekey file, because we want to run this docker image multiple times
# in parallel in the same ethereum network
RUN rm -f ~/.ethereum/geth/nodekey

# Create an initial account using the password from the environment
RUN echo ${INITIAL_ACCOUNT_PASSWORD} > /tmp/password \
    && geth account new --password /tmp/password \
    && rm -f /tmp/password

ENTRYPOINT ["geth"]
