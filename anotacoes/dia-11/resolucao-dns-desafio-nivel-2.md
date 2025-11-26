# Resolução de DNS

Do meu computador, quero acessar um site que está hospedado remotametne (TabNews). Pra isso, só precisamos do IP dele, mas não sabemos isso, a única coisa que temos é o nome do domínio (TabNews.com.br).

Quando digitamos esse domínio na internet, o OS faz uma requisição para o provedor de internet, que possui um recurso chamado `Recursive Resolver`, e ele tenta descobrir qual é esse IP.

A única informação que o provedor possui (que tá, de certa forma, hard coded nele) é quais são os IPs dos `Root servers`, que são 13 servidores (13 pontos de entrada) espalhados pelo mundo. A redundância deles é garantida pelas suas mais de 1.700 instâncias.

O provedor pergunta pro root server, e o root server olha para o "tipo" do domínio (.com.br, .eng, .org, etc...), e com base nisso, ele já sabe qual instância vai ter essa informação.

O domínio, exatamente como ele é, pode ser divido dessa forma:

```
tabnews.com.br. // Sim, tem um ponto no final
```

1 - Aquele ponto no final é o root domain, é através dele que o Root Server sabe por onde começar a ler o domínio.

2 - Depois, da direita pra esquerda, temos o `TLD` (Top-Level Domain), que é o `.br`. E essa é a única que os roots sabem: onde estão os servidores responsáveis por cada TLD.

Existem duas categorias de TLDs:

- ccTLDs: são os TLDs separados para so países (country code - .br pro Brasil, .ca pro Canadá, .pt pra Portugal), etc;
- gTLDs: TLDs genéricos, como o `.com` (commercial), .org, .net, .dev, .bradesco...

Uma vez identificado o TLD, o Root Serve devolve para o Recursive Resolver uma lista com os IPs de quem gerencia aquele TLD.

3 - O recursive resolver então pergunta "Quem tem o IP desse domínio?" E ele também não sabe, mas ele devolve um IP pra um outro servidor chamado de `Authoritative Server`, e ele sim possui todos os registros do seu domínio. Esse domínio pode estar armazenado como um alias, um cname, txt, mx, etc... E aí sim, ele consegue esse IP.

Como pode-se imaginar, esse processo todo demora bastante, e é apenas um entre tantos outros que acontecem de forma sequencial ou paralela. E frequentemente, o IP desejado não muda, então é pouco eficiente ficar recalculando a mesma coisa várias vezes.

Para tentar diminuir esse desperdício, criou-se algo chamado `TTL` (Time To Live), que diz por quanto tempo uma informação pode ser considerada válida, ou seja, quanto tempo ela pode ser mantida em cache. E esse TTL é aplicado em todas as etapas do processo envolvendo `Recursive Resolver`, `Root Server`, `TLD Server` e `Authoritative Server`, o próprio provedor e a nossa máquina.
