# 🚀 TaxAssistantApp - Uproszczone Wdrożenie

Wdróż aplikację TaxAssistantApp w swojej subskrypcji Azure za pomocą prostego procesu jednym kliknięciem. To wdrożenie tworzy tylko niezbędną infrastrukturę (App Service + Key Vault) bez skomplikowanych integracji.

## ✨ Co zostanie wdrożone

- **Azure App Service** - Hostuje twoją aplikację webową
- **Azure Key Vault** - Bezpiecznie przechowuje klucze API
- **Managed Identity** - Umożliwia aplikacji bezpieczny dostęp do Key Vault

## 📋 Wymagania wstępne

Przed wdrożeniem będziesz potrzebować:

1. **Subskrypcję Azure** - Z uprawnieniami do tworzenia zasobów
2. **Klucz API NSA Search** - Do funkcji wyszukiwania interpretacji podatkowych
3. **Klucz API NSA Detail** - Do pobierania szczegółowych interpretacji

## 🎯 Proces Wdrożenia

### Krok 1: Kliknij Deploy to Azure

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2F19bartek92%2FtaxAssistantApp-deployment%2Fmain%2Fazuredeploy.json)

*[Placeholder zrzutu ekranu: Przycisk Deploy to Azure]*

### Krok 2: Zaloguj się do Azure

Zostaniesz przekierowany do Azure Portal, aby uwierzytelnić się swoim kontem Azure.

*[Placeholder zrzutu ekranu: Ekran logowania Azure]*

### Krok 3: Skonfiguruj Parametry Wdrożenia

Wypełnij formularz wdrożenia swoimi ustawieniami:

| Parametr | Opis | Przykład | Wymagane |
|----------|-----|----------|----------|
| **Subscription** | Twoja subskrypcja Azure | `Moja Subskrypcja Firmowa` | ✅ |
| **Resource Group** | Utwórz nową lub użyj istniejącej | `rg-taxassistant` | ✅ |
| **Region** | Region Azure do wdrożenia | `Poland Central` | ✅ |
| **App Service Plan Name** | Nazwa planu hostingowego | `taxassistant-plan` | ✅ |
| **Web App Name** | Nazwa twojej aplikacji | `taxassistant-mojafirma` | ✅ |
| **SKU** | Rozmiar planu hostingowego | `F1` (warstwa darmowa) | ✅ |
| **NSA Search API Key** | Twój klucz API do wyszukiwania | `twoj-klucz-search-tutaj` | ✅ |
| **NSA Detail API Key** | Twój klucz API do szczegółów | `twoj-klucz-detail-tutaj` | ✅ |
| **Key Vault Name** | Nazwa dla bezpiecznego magazynu | `kv-taxassistant` | ✅ |

*[Placeholder zrzutu ekranu: Formularz wdrożenia z wypełnionymi parametrami]*

### Krok 4: Przejrzyj i Utwórz

1. Zaznacz "Akceptuję warunki i zasady wymienione powyżej"
2. Kliknij **"Review + create"**
3. Przejrzyj swoje ustawienia
4. Kliknij **"Create"**

*[Placeholder zrzutu ekranu: Ekran przeglądu i tworzenia]*

### Krok 5: Poczekaj na Wdrożenie

Wdrożenie zazwyczaj trwa 3-5 minut. Zobaczysz ekran postępu.

*[Placeholder zrzutu ekranu: Wdrożenie w toku]*

### Krok 6: Wdrożenie Zakończone

Po zakończeniu zobaczysz komunikat o sukcesie z wynikami wdrożenia.

*[Placeholder zrzutu ekranu: Wdrożenie zakończone z rezultatami]*

## 📥 Pobierz Profil Publikacji

Po zakończeniu wdrożenia musisz pobrać profil publikacji, aby wysłać go do developera:

1. Przejdź do **Azure Portal** → **App Services**
2. Znajdź i kliknij na swoją wdrożoną aplikację (np. `taxassistant-abc123`)
3. W sekcji **Overview**, kliknij **"Download publish profile"**
4. Zapisz plik `.pubxml`

*[Placeholder zrzutu ekranu: Przegląd App Service z podświetlonym przyciskiem pobierania]*

## 📧 Wyślij do Developera

**⚠️ Ważne: Obsługuj bezpiecznie!**

Profil publikacji zawiera dane uwierzytelniające do wdrożenia. Proszę:

1. **Zaszyfruj plik** lub użyj bezpiecznej usługi udostępniania plików
2. **Wyślij bezpieczną metodą** (zaszyfrowany email, zip z hasłem, itp.)
3. **Dołącz te informacje:**
   - Nazwa Resource Group
   - Nazwa Web App
   - Wszelkie specjalne wymagania

### Szablon Email
```
Temat: TaxAssistantApp Wdrożenie - Profil Publikacji

Cześć [Developer],

Pomyślnie wdrożyłem infrastrukturę TaxAssistantApp na Azure.

Szczegóły Wdrożenia:
- Resource Group: [nazwa-twojej-grupy-zasobów]
- Web App Name: [nazwa-twojej-aplikacji]
- App URL: [url-twojej-aplikacji]

W załączniku znajdziesz profil publikacji (zaszyfrowany/zabezpieczony hasłem).
Hasło: [jeśli dotyczy]

Infrastruktura jest gotowa do wdrożenia aplikacji.

Pozdrawiam,
[Twoje imię]
```

## 🔧 Instrukcje dla Developera

Dla developera wdrażającego aplikację:

1. **Wyodrębnij** plik profilu publikacji
2. **Zbuduj** aplikację: `dotnet publish -c Release -o ./publish`
3. **Wdróż** używając Azure CLI:
   ```bash
   az webapp deploy \
     --resource-group [nazwa-grupy-zasobów] \
     --name [nazwa-aplikacji] \
     --src-path ./publish \
     --type zip
   ```

## 🌐 Dostęp do Twojej Aplikacji

Po wdrożeniu kodu przez developera, twoja aplikacja będzie dostępna pod adresem:
```
https://[nazwa-twojej-aplikacji].azurewebsites.net
```

## ❓ Rozwiązywanie Problemów

### Częste Problemy

**P: Wdrożenie kończy się niepowodzeniem z "Key Vault name not available"**
O: Nazwy Key Vault muszą być globalnie unikalne. Spróbuj innej nazwy lub pozwól systemowi wygenerować jedną.

**P: Nie mogę pobrać profilu publikacji**
O: Warstwa F1 (darmowa) ma ograniczone opcje publikacji. Nadal możesz wdrażać używając Visual Studio Code z rozszerzeniem Azure lub Azure CLI z centrum wdrożenia.

**P: Aplikacja pokazuje błąd po wdrożeniu**
O: Infrastruktura została utworzona, ale kod aplikacji musi zostać wdrożony przez developera.

**P: Klucze API nie działają**
O: Sprawdź dwukrotnie, czy wprowadziłeś poprawne klucze API NSA podczas wdrożenia.

### Uzyskiwanie Pomocy

Jeśli napotkasz problemy:

1. Sprawdź Azure Portal → Resource Group → Deployments dla szczegółów błędu
2. Skontaktuj się ze swoim developerem z komunikatem błędu
3. Upewnij się, że wszystkie wymagane parametry zostały wypełnione poprawnie

## 🔒 Notatki Bezpieczeństwa

- Klucze API są bezpiecznie przechowywane w Azure Key Vault
- Aplikacja używa Managed Identity do dostępu do sekretów
- Wszystkie połączenia używają HTTPS
- Profil publikacji zawiera tymczasowe dane uwierzytelniające wdrożenia

## 💰 Szacowanie Kosztów

Szacowany miesięczny koszt dla planu F1 w Polsce Centralnej:
- **App Service Plan (F1)**: DARMOWY (z ograniczeniami)
- **Key Vault**: ~2 zł/miesiąc (za operacje na sekretach)
- **Razem**: ~2 zł/miesiąc

*Ograniczenia F1: 60 minut czasu obliczeniowego dziennie, 1GB miejsca na dysku, brak domen niestandardowych*

*Uwaga: Koszty mogą się różnić w zależności od regionu i użycia. Sprawdź kalkulator cen Azure dla dokładnych szacunków.*

---

## 📞 Wsparcie

W przypadku wsparcia technicznego lub pytań dotyczących tego procesu wdrożenia, skontaktuj się ze swoim zespołem deweloperskim.

**Miłego wdrażania!** 🎉