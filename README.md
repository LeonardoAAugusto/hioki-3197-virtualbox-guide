# hioki-3197-virtualbox-guide
Guide and assets for running Hioki 3197 Power Quality Analyzer software (v1.02) on modern 64-bit systems via Windows XP VirtualBox VM.

# Hioki 3197 (Ver 1.02) on Modern Windows (64-bit) via VirtualBox & Windows XP

Repositório técnico dedicado a documentar o processo completo de instalação, configuração e execução do software legado **Hioki 3197 (Ver 1.02)** e respetivas dependências num hospedeiro Windows moderno de 64-bit, utilizando uma máquina virtual com **Windows XP Professional SP3 (x86)**.

---

## 1. Pré-Requisitos e Downloads Necessários

Antes de iniciar o processo de configuração, certifique-se de descarregar e preparar os seguintes componentes:

- **Oracle VM VirtualBox:**
  - Aceda ao site oficial: [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
  - Selecione a opção **Windows hosts** (ou a versão correspondente ao seu sistema operativo hospedeiro) e conclua a instalação do software de virtualização no seu computador principal.

- **Imagem ISO do Windows XP (PT-BR):**
  - O sistema operativo convidado necessário é o Windows XP Professional com Service Pack 3 (32-bit).
  - Pode descarregar a imagem ISO oficial em português do Brasil através do Archive.org: [https://archive.org/download/WinXPProSP3PortugueseBrazilian](https://archive.org/download/WinXPProSP3PortugueseBrazilian)
  - O ficheiro exato necessário é o **`pt-br_windows_xp_professional_with_service_pack_3_x86_cd_vl_x14-74137.iso`** (Link direto para download: [https://archive.org/download/WinXPProSP3PortugueseBrazilian/pt-br_windows_xp_professional_with_service_pack_3_x86_cd_vl_x14-74137.iso](https://archive.org/download/WinXPProSP3PortugueseBrazilian/pt-br_windows_xp_professional_with_service_pack_3_x86_cd_vl_x14-74137.iso)).

- **Pacote de Instaladores do Hioki (Disponível neste Repositório):**
  - Descarregue o arquivo **`HIOKI_ENGLISH`** presente neste repositório. Ele contém todos os instaladores necessários: o ambiente Java e os componentes de software da Hioki.

---

## 2. Criação e Configuração da Máquina Virtual no VirtualBox

1. Abra o **VirtualBox** e clique em **Nova** para criar uma nova máquina virtual com os seguintes parâmetros recomendados:
   - **Nome:** `Hioki-3197`
   - **Versão:** `Windows XP (32-bit)`
   - **Memória RAM:** `1024 MB` (1 GB)
   - **Disco Rígido:** Criar um novo disco rígido virtual de pelo menos `10 GB` (alocação dinâmica).
2. Nas definições da máquina virtual criada, vá na secção de Armazenamento, selecione o leitor ótico vazio e insira a imagem ISO do Windows XP (`pt-br_windows_xp_professional_with_service_pack_3_x86_cd_vl_x14-74137.iso`).
3. Inicie a máquina virtual e proceda à instalação padrão do Windows XP (formatação rápida do disco virtual, definições regionais e configuração típica de rede com o grupo de trabalho `WORKGROUP`).

---

## 3. O "Método ISO" para Transferência de Ficheiros

Devido às limitações de compatibilidade de rede e ferramentas de integração (Guest Additions) com o Windows XP nativo, o método mais fiável para passar os instaladores do computador principal para a máquina virtual é transformar os ficheiros numa nova imagem ISO:

1. Extraia o conteúdo do arquivo **`HIOKI_ENGLISH`** descarregado deste repositório para uma pasta no seu computador principal (por exemplo, chame-lhe `Instaladores_Hioki`).
2. Utilize a ferramenta portátil **[Folder2ISO](https://github.com/imgdrive/Folder2ISO)** para converter essa pasta num ficheiro de imagem virtual:
   - **Select Folder:** Selecione a pasta `Instaladores_Hioki`.
   - **Select Output:** Escolha um diretório de destino fora da pasta de origem (ex: Ambiente de Trabalho) e atribua um nome ao ficheiro (ex: `hioki.iso`).
   - Clique em **Generate ISO**.
3. No VirtualBox, com o Windows XP em execução, vá ao menu superior da janela e clique em **Dispositivos > Discos Ópticos > Escolher um ficheiro de disco...**, selecionando o ficheiro `hioki.iso` que acabou de gerar.

---

## 4. Instalação do Software no Windows XP

1. Dentro do Windows XP, abra o **Meu Computador** e aceda à unidade de CD/DVD virtual onde a ISO está montada.
2. **Passo Obrigatório (Dependência de Java):** Navegue até à pasta correspondente, execute o instalador do Java **`j2re-1_4_2_09-windows-i586-p.exe`** e conclua a instalação.
3. **Instalação do Hioki:** Em seguida, aceda à pasta do software da Hioki e execute o ficheiro **`setup.exe`**. Siga os passos indicados no ecrã para finalizar a instalação.

---

## 5. Utilização do Software

Após a instalação concluída com sucesso, aceda ao menu **Iniciar > Todos os Programas > HIOKI > 3197Applications**:
- **3197Communicator:** Utilizado para estabelecer ligação com o instrumento físico Hioki 3197 via USB/Serial, configurar parametrizações e descarregar os dados de registo de energia.
- **3197DataViewer:** Utilizado para analisar os gráficos, relatórios e dados extraídos de forma autónoma.

> **Dica de Comunicação USB:** Para que o Windows XP detete o analisador físico conectado à porta USB do seu PC hospedeiro, aceda ao menu superior do VirtualBox em **Dispositivos > USB** e selecione o dispositivo da Hioki correspondente para o redirecionar para a máquina virtual.
