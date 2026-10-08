# NDD Printer M-Manager

Userscript para o **NDD Print Portal 360** (`https://360.nddprint.com/printers`) que adiciona um painel de gestão em massa da lista de impressoras.

## Instalação

1. Instale um gerenciador de userscripts no navegador:

   | Navegador | Gerenciadores |
   |---|---|
   | Chrome, Edge e outros baseados em Chromium | [Tampermonkey](https://www.tampermonkey.net/) ou [Violentmonkey](https://violentmonkey.github.io/) |
   | Firefox | [Greasemonkey](https://addons.mozilla.org/firefox/addon/greasemonkey/), [Tampermonkey](https://www.tampermonkey.net/) ou [Violentmonkey](https://violentmonkey.github.io/) |

2. Abra o link abaixo. O gerenciador mostra a tela de instalação; confirme em **Instalar**.

   **[Instalar o NDD Printer M-Manager](https://raw.githubusercontent.com/maiconjs/ndd-printer-m-manager/main/ndd-printer-m-manager.user.js)**

3. Acesse `https://360.nddprint.com/printers` (ou recarregue a página). O painel aparece no canto da tela.

### Chrome e Edge (Chromium): liberar a execução de userscripts

Nas versões atuais dos navegadores baseados em Chromium, extensões como o Tampermonkey só executam scripts depois que a permissão é liberada para elas:

- **Chrome / Edge 138 ou mais recente:** abra os detalhes da extensão (botão direito no ícone do Tampermonkey → **Gerenciar extensão**, ou `chrome://extensions` / `edge://extensions` → **Detalhes**) e ative **Permitir scripts de usuário** (*Allow User Scripts*). A opção é por extensão.
- **Versões anteriores à 138, ou se a opção acima não aparecer:** ative o **Modo do desenvolvedor** no canto superior de `chrome://extensions` (ou `edge://extensions`).

Se o painel não aparecer no portal, confira essa permissão primeiro.

## Recursos

- **Seleção em massa**: visíveis, todas as páginas, portas USB, impressoras sem fila, por fabricante/modelo, com janela de revisão e filtros por coluna no estilo Excel.
- **Contabilização em lote**: status, origem (Padrão do sistema, Física e Lógica, Apenas Lógica, Apenas Física com MF/Client Collector) e forçar cor. Escolher uma origem com o status em "manter" habilita as impressoras desabilitadas na mesma gravação.
- **Coluna Origem**: coleta sob demanda, com cache por cliente conferido pela auditoria do NDD (só relê o que mudou).
- **Lista de séries (contrato)**: carrega `.csv`/`.txt`, compara com todas as impressoras do NDD, destaca as que estão fora da lista e as séries da lista que não existem no NDD.
- **Exclusão em massa**: desabilita a contabilização e exclui, acompanhando a fila de liberação do servidor.
- **Ambiente**: filas de impressão por impressora e janela de hosts/produtos NDD com situação de comunicação.
- **Grade**: colunas redimensionáveis com larguras lembradas, exportação `.csv` (abre direto no Excel) e log persistente até fechar a aba.

## Observações

- Usa a mesma sessão do portal (as chamadas à API são feitas com o login atual); não armazena credenciais.
- Ações que alteram dados (contabilização e exclusão) sempre pedem confirmação e registram o resultado no log.
- Exclusão bloqueada por `@@360PrinterCounterStatusIsEnabled` depende de desabilitar o contador no NDD MPS; não há como fazer isso pelo Portal 360.
