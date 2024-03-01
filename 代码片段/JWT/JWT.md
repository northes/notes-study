## 保留字段

- [JSON Web Token (JWT)](https://www.iana.org/assignments/jwt/jwt.xhtml#claims)


## 释义

JWT 规范定义了七个保留声明，这些声明不是必需的，但建议允许与第三方应用程序进行互操作。这些都是：

iss (issuer): Issuer of the JWT
iss （发行者）：JWT 的发行者

sub (subject): Subject of the JWT (the user)
sub （主题）：JWT 的主题（用户）

aud (audience): Recipient for which the JWT is intended
aud （受众）：JWT 的目标接收者

exp (expiration time): Time after which the JWT expires
exp （过期时间）：JWT 过期的时间

nbf (not before time): Time before which the JWT must not be accepted for processing
nbf （不在时间之前）：不得接受 JWT 进行处理的时间

iat (issued at time): Time at which the JWT was issued; can be used to determine age of the JWT

jti (JWT ID): Unique identifier; can be used to prevent the JWT from being replayed (allows a token to be used only once)
jti （JWT ID）：唯一标识符；可用于防止 JWT 被重放（允许令牌仅使用一次）