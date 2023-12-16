To determine your ingress host and port:
export INGRESS_NAME=istio-ingressgateway
export INGRESS_NS=istio-system
kubectl get svc "$INGRESS_NAME" -n "$INGRESS_NS"

Test the gateway with an invalid token:
curl --header "Authorization: Bearer deadbeef" "$INGRESS_HOST:$INGRESS_PORT/headers" -s -o /dev/null -w "%{http_code}\n"

Test the the gateway with a valid token:
TOKEN=$(curl https://raw.githubusercontent.com/istio/istio/release-1.19/security/tools/jwt/samples/demo.jwt -s)
curl --header "Authorization: Bearer $TOKEN" "$INGRESS_HOST:$INGRESS_PORT/headers" -s -o /dev/null -w "%{http_code}\n"