# Chegou Inteiro

Plataforma para consultar experiências de entrega por CEP, loja e modalidade. Quando a participação estiver habilitada, consumidores podem enviar relatos sujeitos à moderação.

## Arquitetura

- **Aplicação:** monólito modular em ASP.NET Core MVC sobre .NET 10.
- **Persistência:** Entity Framework Core 10 e SQL Server.
- **Módulos:** contas, relatos e moderação, comunicação, mapa/geocodificação e operações.
- **Interface:** Bootstrap 5.3 e Leaflet.
- **Integrações documentadas:** ViaCEP, geocodificação, provedores de mapas, SMTP e reCAPTCHA opcional.
- **Operação:** publicação em Docker, health checks e fluxo controlado de release.

## Decisões de engenharia

- Consultas de CEP usam POST; o valor armazenado é protegido pelo ASP.NET Data Protection.
- O código do pedido/rastreio não é persistido. A prevenção de duplicidade usa HMAC-SHA256 com chave protegida.
- Relatos passam por moderação. Comprovantes são opcionais, ficam fora da pasta pública e só são servidos após aprovação.
- Consultas do mapa usam agregação regional e não retornam CEP completo nem dados de usuários.
- Uma combinação só é publicada após atingir o mínimo de cinco consumidores distintos. Esse limite é um piso de agregação; não garante anonimização completa nem representatividade estatística.
- A aplicação mantém os módulos em um único processo e assembly: é um monólito modular, não uma arquitetura de microsserviços.

## Estado da demonstração

A instância pública está em modo de consulta, com novos cadastros e relatos desativados. Os dados de demonstração permitem explorar a interface, mas não comprovam cobertura, adoção ou qualidade real das entregas.

## Acesso

[Abrir a demonstração](https://chegouinteiro.devforyou.com.br/)
