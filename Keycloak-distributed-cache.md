## Cơ chế HA của Keycloak
Keycloak được thiết kế để đảm bảo tính HA và có thể cài đặt thành cụm nhiều nodes. Hiện tại, Keycloak sử dụng cơ chế **distributed-caching** được xây dựng trên **Infinispan** (an open-source, distributed, in-memory key-value data store). Khi chạy ở production mode, caching được sử dụng và tất cả các Keycloak instances trong cùng mạng sẽ được phát hiện. Theo mặc định, caches đang sử dụng là **UDP transport stack**. Các instances sẽ được phát hiện bằng cách dùng **IP multicast transport** dựa trên **UDP**. Tuy nhiên, có các **transport stack** khác thay thế cho **UDP stack** mặc định.

## Các `Transport Stack` mà Keycloak hỗ trợ
Các **transport stacks** đảm bảo các distributed cache nodes trong cùng một cluster có thể liên lạc được với nhau một cách tin cậy. Keycloak hỗ trợ nhiều loại **transport stacks**:
- tcp
- udp
- kubernetes
- ec2
- azure
- google

Chi tiết cách sử dụng từng loại stack ở trên có thể đọc tại [docs](https://www.keycloak.org/server/caching) của Keycloak.

Ngoài ra, có thể tự định nghĩa **transport stack** mới để đáp ứng được với yêu cầu thực tế. Hiện tại, Viettel Cloud đang sử dụng JDBC-PING cho distributed caching.

![image](./images/Screenshot%20from%202023-10-03%2010-27-48.png)

## Ongoing
- Triển khai cụm Keycloak sử dụng JDBC-PING ([Keycloak Cluster using JDBC-PING for Distributed Caching - Medium](https://medium.com/@ivangfr/keycloak-cluster-using-jdbc-ping-for-distributed-caching-8ba5c09cc206))
- Thử nghiệm các transport stacks khác