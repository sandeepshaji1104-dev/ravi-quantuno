[![self-test** cada passo no plano certo e **verifica trivalentemente**
após cada passo — 1 = verificado e segue, 0 = recupera com uma retentativa,
REFUSED = aborta. O pensamento completo (plano + vereditos por passo) vai
selado no recibo de cada missão.

**Não é um chatbot.** É um kernel de operações quânticas que roda
headless em CI: recebe missões, sintetiza circuitos em múltiplas linguagens,
executa em simuladores e em hardware real da IBM, decide em lógica trivalente
ZYQL (1 / 0 / REFUSED) e sela cada missão com recibo pós-quântico Z-QEA v2
(SHA3-256 + assinatura **ML-DSA-44, FIPS 204** + entropia quântica atestada).

Nada silencioso: toda missão produz recibo verificável offline, sem servidor,
sem chave — a chave pública ML-DSA-44 vem dentro do recibo.

## O que ele faz hoje (v1.0.0 — tudo testado)

| Missão | O que executa | Provedor |
|---|---|---|
| `trivalente` | bateria de decisão trivalente (1/0/REFUSED) — Deutsch-Jozsa n=2 | `local` \| `ibm` |
| `poliglota` | o MESMO circuito sintetizado e executado em **Qiskit, OpenQASM 3, Cirq, PennyLane e Braket** — veredito de concordância | `local` |
| `braid` | trançados S3 não-abelianos — prova que a ordem importa (não-comutatividade) | `local` \| `ibm` |
| `entropia` | colheita de entropia em hardware real (QRNG, 32 qubits Hadamard) | `ibm` |
| `catalogo` | survey do conhecimento do agente: linguagens, SDKs, provedores de hardware | `local` |
| `triplanar` | **a missão-assinatura**: os três planos numa só missão (cadeia clássica → bateria quântica → assinatura pós-quântica), com o pensamento do cérebro no recibo | `local` \| `ibm` |

Uso direto:

```bash
pip install pqcrypto qiskit cirq pennylane amazon-braket-sdk
python3 ravi_quantuno.py --mission examples/missoes/poliglota.json
```

Uso como GitHub Action:

```yaml
- uses: SerenaSolutions/ravi-quantuno@v1
  with:
    mission: ravi/trivalente.json   # arquivo de missão do seu repo
    provider: ibm                    # requer secret ZYQL_TOKEN
```

Saídas: `verdict` (trivalente — recusa quebra o build), `receipt-file`, `seal`.

## Conhecimento do agente (módulo `ravi/knowledge.py`)

Catálogo versionado do ecossistema quântico: **14 linguagens/SDKs catalogados**
(5 executáveis no kernel hoje: Qiskit, OpenQASM 3, Cirq, PennyLane, Braket;
Q#, Quil/pyQuil, Stim, tket, Silq, Ocean, ProjectQ, Mitiq e QuTiP como
referência/roteiro), **provedores de hardware e nuvem** (IBM Quantum em
produção; Amazon Braket local; Azure Quantum, IonQ, Quantinuum, OQC, Rigetti,
Pasqal, QuEra, D-Wave no roteiro) e a stack da casa (ZEPHIRUM/ZYQL/Z-QEA).

Declaração honesta: o kernel é determinístico — não embute LLM. A camada de
raciocínio aberto (planejamento de missões por linguagem natural) entra pela
Serena Quantum API, com o token trancado no servidor, nunca no app.

## Arquitetura de segurança da casa

1. **Nenhum token no código.** Hardware IBM só via `ZYQL_TOKEN` no ambiente
   (secret do CI). O recibo registra o job ID, jamais a credencial.
2. **Recibos pós-quânticos Z-QEA v2**: SHA3-256 (Grover-resistente) +
   ML-DSA-44 (FIPS 204) — nenhum computador quântico falsifica um recibo do Ravi.
3. **Trivalência radical**: veredito `REFUSED` encerra a missão com erro —
   o agente não "continua mesmo assim".

## Por que é exclusivo

1. **Triplanar**: clássico + quântico + pós-quântico no mesmo kernel — não
   existe outro agente de operações com isso.
2. **Núcleo trivalente**: lógica 1/0/REFUSED herdada do ZYQL — um agente que
   sabe recusar (nenhum LLM do mercado é trivalente por núcleo).
3. **Pensamento auditável**: o plano e os vereditos de cada passo vão no recibo
   selado — autonomia com prova, não autonomia cega.
4. **Nada silencioso**: recibo pós-quântico em toda missão, verificável offline.

## Missão de estreia (hardware real)

A primeira missão do Ravi Quantuno rodou no silício da IBM: ve
