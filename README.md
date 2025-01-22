### Azure DevOps Agent Kurulum Rehberi (Rocky Linux)

Bu rehber, Rocky Linux üzerinde Azure DevOps Agent kurulumunu adım adım açıklamaktadır.

---

## Ön Koşullar:
1. **Sistemin güncel olduğundan emin olun:**
   ```bash
   sudo dnf update -y
   ```
   *Neden*: Sistem güncellemeleri, potansiyel hataları önler ve güvenliği artırır.

2. **Yeni Kullanıcı Oluşturma:** Azure DevOps Agent için ayrı bir kullanıcı oluşturun.
   ```bash
   sudo useradd -m azureagent
   sudo passwd azureagent
   ```
   *Neden*: Root yetkilerini doğrudan kullanmak yerine ayrı bir kullanıcı güvenlik açısından önemlidir.

3. **Kullanıcıya Gerekli Yetkileri Verme:**
   ```bash
   sudo usermod -aG wheel azureagent
   ```
   *Neden*: Kullanıcının gerekli yönetimsel işlemleri gerçekleştirmesi için yetki verir.

---

## Azure DevOps Agent Kurulum Adımları:

1. **Agent Paketini İndirme:**
   ```bash
   curl -O https://vstsagentpackage.azureedge.net/agent/3.225.0/vsts-agent-linux-x64-3.225.0.tar.gz
   ```
   *Neden*: Azure DevOps Agent'ın kurulum dosyasını indirir.

2. **Agent Dosyasını Çıkarma:**
   ```bash
   mkdir -p /home/azureagent/azagent
   tar -xzf vsts-agent-linux-x64-3.225.0.tar.gz -C /home/azureagent/azagent
   ```
   *Neden*: Dosyayı kurulum için hazırlamak gerekir.

3. **Kullanıcı Sahipliğini Ayarlama:**
   ```bash
   sudo chown -R azureagent:azureagent /home/azureagent/azagent
   ```
   *Neden*: Doğru izinlerin sağlanması gerekir.

4. **Agent'ı Yapılandırma:**
   ```bash
   su - azureagent
   cd /home/azureagent/azagent
   ./config.sh
   ```
   *Neden*: Azure DevOps ile bağlantı kurmak için yapılandırma gereklidir.

5. **Agent Hizmetini Başlatma:**
   ```bash
   sudo ./svc.sh install
   sudo ./svc.sh start
   ```
   *Neden*: Agent'ı bir sistem hizmeti olarak çalıştırır.

---

## Kontrol ve Doğrulama:

1. **Agent Durumunu Kontrol Etme:**
   ```bash
   systemctl status vsts.agent.*
   ```
   *Neden*: Agent'ın düzgün çalışıp çalışmadığını kontrol eder.

2. **Azure DevOps Portal Doğrulaması:**
   Azure DevOps portalına giderek Agent'ın bağlı olup olmadığını kontrol edin.

---

Bu adımlar takip edilerek Rocky Linux üzerinde Azure DevOps Agent kurulumu tamamlanabilir. Herhangi bir sorunla karşılaşırsanız, destek almak için iletişime geçebilirsiniz.




