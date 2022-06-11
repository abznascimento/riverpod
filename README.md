<p align="center">
<a href="https://github.com/rrousselGit/river_pod/actions"><img src="https://github.com/rrousselGit/river_pod/workflows/Build/badge.svg" alt="Build Status"></a>
<a href="https://codecov.io/gh/rrousselgit/river_pod"><img src="https://codecov.io/gh/rrousselgit/river_pod/branch/master/graph/badge.svg" alt="codecov"></a>
<a href="https://github.com/rrousselgit/river_pod"><img src="https://img.shields.io/github/stars/rrousselgit/river_pod.svg?style=flat&logo=github&colorB=deeppink&label=stars" alt="Star on Github"></a>
<a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/license-MIT-purple.svg" alt="License: MIT"></a>
<a href="https://discord.gg/Bbumvej"><img src="https://img.shields.io/discord/765557403865186374.svg?logo=discord&color=blue" alt="Discord"></a>

<p align="center">
<a href="https://www.netlify.com">
  <img src="https://github.com/ulisseshen/riverpod/blob/master/resources/githubpages_host.png?raw=true" alt="Hospedado por github pages" />
</a>
</p>

<p align="center">
<img src="https://github.com/ulisseshen/riverpod/blob/master/resources/icon/Facebook%20Cover%20A.png?raw=true" width="100%" alt="Riverpod" />
</p>

</p>

---

Uma biblioteca de gerenciamento de estado que:

- detecta erros de programação em tempo de compilação e não em tempo de execução
- remove o aninhamento para ouvir/combinar objetos
- garante que o código seja testável

| riverpod         | [![pub package](https://img.shields.io/pub/v/riverpod.svg?label=riverpod&color=blue)](https://pub.dartlang.org/packages/riverpod)                 |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| flutter_riverpod | [![pub package](https://img.shields.io/pub/v/riverpod.svg?label=flutter_riverpod&color=blue)](https://pub.dartlang.org/packages/flutter_riverpod) |
| hooks_riverpod   | [![pub package](https://img.shields.io/pub/v/riverpod.svg?label=hooks_riverpod&color=blue)](https://pub.dartlang.org/packages/hooks_riverpod)     |

Bem-vindo ao [Riverpod]!

Este projeto pode ser considerado como uma reescrita do [provider] para fazer melhorias que de outra forma seriam impossíveis.

Para aprender a usar o [Riverpod], consulte sua documentação: https://ulisseshen.github.io/riverpod/

Resumo:

- Declare seus providers como variáveis globais:

  ```dart
  final counterProvider = StateNotifierProvider((ref) {
    return Counter();
  });

  class Counter extends StateNotifier<int> {
    Counter(): super(0);

    void increment() => state++;
  }
  ```

- Use-os dentro de seus widgets de maneira segura em tempo de compilação. Sem exceções de tempo de execução!

  ```dart
  class Example extends ConsumerWidget {
    @override
    Widget build(BuildContext context, WidgetRef ref) {
      final count = ref.watch(counterProvider);
      return Text(count.toString());
    }
  }
  ```

Veja o [FAQ](#FAQ) se você tiver dúvidas sobre o que isso significa [provider].

## Migração

Com o lançamento da versão 1.0.0, a sintaxe para interagir com providers mudou.

Consulte [o guia de migração](https://ulisseshen.github.io/riverpod/docs/migration/0.14.0_to_1.0.0/) para obter mais informações

## Índice

- [Migração](#migration)
- [Índice](#index)
- [Motivação](#motivation)
- [Contribuindo](#contributing)
- [FAQ](#faq)
  - [Por que outro projeto quando provider já existe?](#why-another-project-when-provider-already-exists)
  - [É seguro usar em produção?](#is-it-safe-to-use-in-production)
  - [Será mesclado com o provider em algum momento?](#will-this-get-merged-with-provider-at-some-point)
  - [Provider será depreciado/parará de ser suportado?](#will-provider-be-deprecatedstop-being-supported)
- [Patrocinadores](#sponsors)

## Motivação

Se [provider] é uma simplificação de [InheritedWidget]s, então [Riverpod] é uma reimplementação de [InheritedWidget]s do zero.

É muito semelhante ao [provider] em princípio, mas também tem grandes diferenças como uma tentativa de corrigir os problemas comuns que esse [provider] enfrenta.

[Riverpod] tem vários objetivos. Primeiro, ele herda os objetivos do [provider]:

- Ser capaz de criar, observar e descartar estados com segurança sem ter que se preocupar em perder o estado na reconstrução (rebuild) do widget.
- Tornando nossos objetos visíveis no devtool do Flutter por padrão.
- Testável e combinável
- Improve the readability of [InheritedWidget]s when we have multiple of them
  (which would naturally lead to a deeply nested widget tree).
- Make apps more scalable with a unidirectional data flow.

From there, [Riverpod] goes a few steps beyond:

- Reading objects is now **compile-safe**. No more runtime exception.
- It makes the [provider] pattern more flexible, which allows supporting commonly
  requested features like:
  - Being able to have multiple providers of the same type.
  - Disposing the state of a provider when it is no longer used.
  - Have computed states
  - Making a provider private.
- Simplifies complex object graphs. It is easier to depend on asynchronous state.
- Makes the pattern independent from Flutter

These are achieved by no longer using [InheritedWidget]s. Instead, [Riverpod]
implements its own mechanism that works in a similar fashion.

For learning how to use [Riverpod], see its documentation: https://riverpod.dev

## Contributing

Contributions are welcomed!

Here is a curated list of how you can help:

- Report bugs and scenarios that are difficult to implement
- Report parts of the documentation that are unclear
- Fix typos/grammar mistakes
- Update the documentation / add examples
- Implement new features by making a pull-request

## FAQ

### Why another project when provider already exists?

While [provider] is largely used and well accepted by the community,
it is not perfect either.

People regularly file issues or ask questions about some problems they face, such as:

- Why do I have a `ProviderNotFoundException`?
- How can I automatically dispose my state when not used anymore?
- How to make a provider that depends on other (potentially complex) providers?

These are legitimate problems, and I believe that something can be improved to fix
those.

The issue is, these problems are deeply rooted in how [provider] works, and
fixing those problems is likely impossible without drastic changes to the
mechanism of [provider].

In a way, if [provider] is a candle then [Riverpod] is a lightbulb. They have
very similar usages, but we cannot create a lightbulb by improving our candle.

### Is it safe to use in production?

Yes.

[Riverpod] is stable and actively maintained.

### Will this get merged with provider at some point?

No. At least not until it is proven that the community likes [Riverpod]
and that it doesn't cause more problems than it solves.

While [provider] and this project have a lot in common, they do have some
major differences. Differences big enough that it would be a large breaking
change for users of [provider] to migrate [Riverpod].

Considering that, separating both projects initially sounds like a better
compromise.

### Will provider be deprecated/stop being supported?

Not in the short term, no.

However, a migration tool is planned to help assist migration from provider
to [Riverpod].

## Sponsors

<p align="center">
  <a href="https://raw.githubusercontent.com/rrousselGit/freezed/master/sponsorkit/sponsors.svg">
    <img src='https://raw.githubusercontent.com/rrousselGit/freezed/master/sponsorkit/sponsors.svg'/>
  </a>
</p>

[provider]: https://github.com/rrousselGit/provider
[riverpod]: https://github.com/rrousselGit/river_pod
[flutter_hooks]: https://github.com/rrousselGit/flutter_hooks
[inheritedwidget]: https://api.flutter.dev/flutter/widgets/InheritedWidget-class.html
[hooks_riverpod]: https://pub.dev/packages/hooks_riverpod
[flutter_riverpod]: https://pub.dev/packages/flutter_riverpod
