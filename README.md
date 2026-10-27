# hioki-3197-virtualbox-guide
Guide and assets for running Hioki 3197 Power Quality Analyzer software (v1.02) on modern 64-bit systems via Windows XP VirtualBox VM.

# Hioki 3197 (Ver 1.02) on Modern Windows (64-bit) via VirtualBox & Windows XP

Repositório técnico dedicado a documentar o processo de instalação, configuração e execução do software legado **Hioki 3197 (Ver 1.02)** e respetivas dependências num hospedeiro Windows moderno de 64-bit, utilizando uma máquina virtual com **Windows XP Professional SP3 (x86)**.

---

## 📋 Contexto do Problema
O software oficial do analisador de qualidade de energia **Hioki 3197 (Ver 1.02)** depende de arquiteturas de 32 bits e bibliotecas obsoletas, sendo incompatível nativamente com sistemas operativos Windows modernos de 64 bits. Para além disso, o software exige obrigatoriamente o **Java Runtime Environment (JRE) 1.4.2**.

---

## 🛠️ Requisitos e Dependências
* **Sistema Hospedeiro (Host):** Windows 10 / 11 (64-bit).
* **Software de Virtualização:** Oracle VM VirtualBox.
* **Sistema Convidado (Guest OS):** Windows XP Professional SP3 (32-bit / x86).
* **Dependências de Software:**
  * Java Runtime Environment (JRE) `j2re-1_4_2-win32.exe`.
  * Hioki 3197 Software (Ver 1.02) – Inclui `3197Communicator` e `3197DataViewer`.
* **Ferramenta de Empacotamento:** Folder2ISO (para criar a imagem ISO de transferência).

---

## 🚀 Guia Passo a Passo de Implementação

### 1. Criação e Configuração da Máquina Virtual (VirtualBox)
1. Crie uma nova máquina virtual no VirtualBox:
   * **Nome:** Hioki-3197
   * **Versão:** Windows XP (32-bit)
   * **Memória RAM:** 1024 MB (1 GB)
   * **Disco Rígido:** 10 GB (Dinamicamente alocado)
2. Insira a imagem ISO de instalação do Windows XP e proceda à instalação padrão (Configurações Típicas de rede, grupo de trabalho `WORKGROUP`).

### 2. O "Método ISO" para Transferência de Ficheiros
Devido às limitações de compatibilidade de rede e ferramentas de integração (Guest Additions) com o Windows XP nativo, o método mais fiável para passar os instaladores do host para a máquina virtual é através de uma imagem ISO virtual:
1. Crie uma pasta no hospedeiro chamada `Instaladores_Hioki`.
2. Coloque lá dentro o instalador do Java (`j2re`) e a pasta com os ficheiros de instalação do Hioki 3197.
3. Utilize a ferramenta portátil **[Folder2ISO](https://github.com/imgdrive/Folder2ISO)**:
   * **Select Folder:** Selecione a pasta `Instaladores_Hioki`.
   * **Select Output:** Escolha um diretório de destino fora da pasta de origem (ex: Ambiente de Trabalho) e defina o nome do ficheiro (ex: `hioki.iso`).
   * Clique em **Generate ISO**.
4. No VirtualBox, com o Windows XP a correr, vá a **Dispositivos > Discos Ópticos > Escolher um ficheiro de disco...** e selecione o ficheiro `hioki.iso` gerado.

### 3. Instalação no Windows XP
1. Dentro do Windows XP, abra o **Meu Computador** e aceda à unidade de CD/DVD virtual onde a ISO está montada.
2. **Passo Obrigatório:** Execute e instale primeiro o **Java JRE 1.4.2**.
3. Em seguida, navegue até à pasta do software Hioki 3197 e execute o instalador (`setup.exe`).

---

## 🖥️ Utilização do Software
Após a instalação concluída, aceda ao menu **Iniciar > Todos os Programas > HIOKI > 3197Applications**:
* **3197Communicator:** Utilizado para ligar o instrumento Hioki 3197 via USB/Serial, configurar parametrizações e descarregar os dados de registo de energia.
* **3197DataViewer:** Utilizado para analisar os gráficos, relatórios e dados extraídos.

> **Dica de Comunicação USB:** Para que o Windows XP detete o analisador físico conectado à porta USB do PC principal, aceda ao menu superior do VirtualBox em **Dispositivos > USB** e selecione o dispositivo da Hioki correspondente.
