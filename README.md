## Adımlar

1. Uygunluk Kontrolü:
   * İlk olarak, projenin [websitesine](https://claim.fluence.network/) gidin ve projenin gereksinimlerine uygun olup olmadığınızı kontrol edin.

2. Git Reposunu Klonlama:
   * Uygun olduğunuzu doğruladıktan sonra, Git reposunu aşağıdaki komut ile klonlayın:
     ```bash
     git clone git@github.com:fluencelabs/dev-rewards.git
     ```

3. Docker ile Repo'yu Build Etme:
   * Klonladığınız repoyu Docker kullanarak build edin. Eğer sisteminizde Docker yüklü değilse, [Docker'ın resmi websitesinden](https://www.docker.com/products/docker-desktop/) indirip kurabilirsiniz.
  
     ```bash
     docker build -t dev-reward-script .
     ```

4. SSH Anahtarlarını Kopyalama:
   * Bilgisayarınızda bulunan SSH anahtarlarını (RSA veya Ed25519) masaüstüne bir klasöre kopyalayın. Bu, Docker konteyneri içinde anahtarlarınıza erişim sağlamak için kullanılacaktır.
     ```bash
     cd ~/.ssh
     cp id_ed25519 ~/Desktop/keyler
     cp id_ed25519.pub ~/Desktop/keyler
     ```

5. Docker Run ile SSH Anahtarları:
   * Docker konteynerini çalıştırırken, SSH anahtarlarının bulunduğu klasörün konumunu belirtin. Örneğin, anahtarlarınız masaüstündeki "keyler" adlı bir klasördeyse, aşağıdaki gibi bir komut kullanın:
     ```bash
     docker run -it --network none -v ~/Desktop/keyler:/root/.ssh:ro dev-reward-script
     ```

     * --network none: Bu seçenek, konteynerin dış ağlara bağlanmasını engeller, güvenlik için kullanılır.
     * -it: Bu seçenek, konteyner içinde interaktif bir terminal başlatır.
     * -v: Bu, Docker'ın bir volume (bir dosya/dizin bağlantısı) oluşturmasını sağlar. Bu durumda, yerel makinenizdeki bir dizini konteyner içinde bir dizine bağlar.

6. GitHub Kullanıcı Adı ve Cüzdan Adresi:
   * Docker konteyneri çalıştırıldıktan sonra, script sizden GitHub kullanıcı adınızı ve tokenleri claim etmek istediğiniz cüzdan adresini soracaktır. Güvenlik için, boş veya az kullanılan bir cüzdan adresi kullanabilirsiniz.
  
7. SSH Anahtar Yolunu Girme:
   * Script "Your ssh keys in ~/.ssh:" altında bir yol gösterecek. Bu yolu kopyalayın ve scripte girin. Örneğin:
     ```bash
     /root/.ssh/id_ed25519
     ```

8. Sonuç ve Claim İşlemi:
   * Script başarıyla tamamlandığında, "Success! Copy the line below and paste it in the fluence airdrop website." şeklinde bir çıktı alacaksınız. Bu çıktıda yer alan proof'u, projenin websitesine girerek token claim işlemini gerçekleştirin.
