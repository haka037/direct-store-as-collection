# 직영점 AS 수거 신청 사이트

직영점 팀장님용 별도 정적 사이트입니다. 이 사이트는 DB에 직접 접속하지 않고 ERP API만 호출합니다.

## 구조

- 정적 사이트: `index.html`
- ERP API 기본 주소: `https://second-erp-production.up.railway.app`
- 저장 원장: ERP DB `ams_as_requests`
- 매장 후보: ERP DB `stores`
- 제품 후보: ERP DB `products`

## 호스팅

Vercel, Netlify, Cloudflare Pages, GitHub Pages 같은 정적 호스팅에 이 폴더를 그대로 올리면 됩니다.

운영 ERP에서 CORS 허용 도메인을 제한하려면 환경변수에 호스팅 주소를 넣습니다.

```bash
DIRECT_STORE_AS_COLLECTION_ALLOWED_ORIGINS=https://your-as-site.example.com
DIRECT_STORE_AS_COLLECTION_PASSCODE=팀장용접속코드
```

여러 도메인은 쉼표로 구분합니다.

```bash
DIRECT_STORE_AS_COLLECTION_ALLOWED_ORIGINS=https://a.example.com,https://b.example.com
```

## 보안 원칙

- DB URL, DB 비밀번호, Prisma 정보는 정적 사이트에 넣지 않습니다.
- 정적 사이트는 `X-Direct-Store-AS-Collection-Passcode` 헤더로 ERP API에 요청합니다.
- ERP API가 접속코드를 검증한 뒤 ERP DB에 저장합니다.
