Recomendo executar nesta ordem:

/distill — Remove decorative noise: orbs (.hero-orb, .cta-orb), particle canvas (#particles), e a animação scroll-hint-line. Deixa o conteúdo clínico respirar.

/quieter — Troca o glassmorphism das annotation cards por cards sólidos com borda sutil. Suaviza os box-shadows excessivos. Calibra o tom visual para clinical-editorial.

/harden — Adiciona hamburger menu mobile + prefers-reduced-motion para o frame carousel + fallback para falha no preload dos frames + fallback para o widget Behold.

/normalize — Corrige o #dde6f0 hardcoded na specs section para o token correto e padroniza os estilos de botão (.btn-primary vs .navbar-cta divergem levemente).

/audit — Resolve os 11 contrast violations detectados automaticamente (footer tagline e labels com opacity < 0.5).

/optimize — Troca transition: width na navbar por transform/max-width para eliminar o layout thrash.

/polish — Passe final antes de migrar: alinhamento, espaçamentos, hierarquia visual após todas as remoções.

Você pode pedir para eu rodar esses um de cada vez, todos de uma vez, ou em qualquer ordem. Re-rode /critique depois para ver o score melhorar.
