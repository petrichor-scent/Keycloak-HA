ARG KC_VERSION=22.0.4
FROM quay.io/keycloak/keycloak:${KC_VERSION} as builder
RUN /opt/keycloak/bin/kc.sh build \
      --features token-exchange \
      --cache-stack=tcp

FROM quay.io/keycloak/keycloak:${KC_VERSION}
COPY --from=builder /opt/keycloak/ /opt/keycloak/
WORKDIR /opt/keycloak
ENTRYPOINT ["/opt/keycloak/bin/kc.sh"]