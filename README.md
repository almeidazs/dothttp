<div align="center">

# AbacatePay HTTP

Coleção oficial de **requisições HTTP** da **AbacatePay** para testar, integrar e entender a API de forma **simples, transparente e sem abstrações**.

Este repositório fornece exemplos reais da API da AbacatePay nos formatos **`.http`**, compatíveis com **VS Code**, **JetBrains IDEs**, **Insomnia** e qualquer ferramenta que suporte HTTP bruto.

<img src="https://res.cloudinary.com/dkok1obj5/image/upload/v1767631413/avo_clhmaf.png" width="100%" alt="AbacatePay Open Source"/>

<br>

Você pode encontrar a documentação completa da API [aqui](https://docs.abacatepay.com/pages/http).

## Requisitos

Você pode usar qualquer uma das opções abaixo:

</div>

- **VS Code** + extensão **REST Client**
- **JetBrains IDEs** (WebStorm, GoLand, IntelliJ, etc.)
- **Insomnia**
- Qualquer cliente HTTP compatível com variáveis

<div align="center">

## Configuração

Crie (ou edite) um arquivo de environment dentro da versão desejada.

Exemplo, `v1/environments/prod.env`.

</div>

```env
API_VERSION=v1
WEBHOOK_SECRET=abc_my_secret
ABACATEPAY_API_KEY=abc_prod_xxx
BASE_URL=https://api.abacatepay.com
BASE_WEBHOOK_URL=http://localhost:3000
```

<div align="center">

## Uso básico

Abra qualquer arquivo **.htt**p e execute a requisição diretamente da sua IDE.

Por exemplo, criar um QRCode PIX na v1

</div>

```http
### Create QRCode PIX

POST {{$dotenv .env BASE_URL}}/{{$dotenv .env API_VERSION}}/pixQrCode/create

Content-Type: application/json
Authorization: Bearer {{$dotenv .env ABACATEPAY_API_KEY}}

{
  "amount": 1000
}
```

<div align="center">

## Webhooks

Os arquivos **.http** também incluem exemplos para simular webhooks localmente.
</div>

```http
### Simular webhook billing.paid
POST {{$dotenv .env BASE_WEBHOOK_URL}}/webhooks/abacatepay?webhookSecret={{$dotenv .env WEBHOOK_SECRET}}

X-Webhook-Signature: ...

{
    "id": "log_12345abcdef",
    "data": {
        "payment": {
            "amount": 1000,
            "fee": 80,
            "method": "PIX"
        },
        "pixQrCode": {
            "amount": 1000,
            "id": "pix_char_mXTWdj6sABWnc4uL2Rh1r6tb",
            "kind": "PIX",
            "status": "PAID"
        }
    },
    "devMode": false,
    "event": "billing.paid"
}
```

<div align="center">

## Quando usar este repositório?

Use este repo se você:

</div>

- Prefere HTTP cru ao invés de SDK
- Quer entender a API sem abstrações
- Precisa debugar requests/responses reais
- Quer exemplos executáveis versionáveis

Se preferir um wrapper de alto nível, veja também: [`@abacatepay/sdk`](https://www.npmjs.com/package/@abacatepay/sdk)

<div align="center">

## Estrutura do repositório

As requisições são **organizadas por versão da API**, respeitando os limites e diferenças entre cada uma.

</div>

```txt
├─ v1/
│  ├─ billing.http
│  ├─ pix.http
│  ├─ payout.http
│  ├─ webhook.http
│  └─ ...
│
├─ v2/
│  ├─ checkout.http
│  ├─ pix.http
│  ├─ payout.http
│  ├─ webhook.http
│  └─ ...
│
└─ .env
└─ README.md
```

<div align="center">

Cada pasta representa uma versão **isolada da API**.
Sem misturar v1 com v2.

Feito com 🥑 pela equipe AbacatePay</br>
Open source, de verdade.
</div>
