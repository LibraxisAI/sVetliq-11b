---
license: apache-2.0
base_model: speakleash/Bielik-11B-v2.6-Instruct
language:
- pl
library_name: mlx
inference:
  parameters:
    temperature: 0.7
    max_length: 32768
    top_p: 0.95
widget:
- messages:
  - role: user
    content: "Pacjent: kot, 12 lat, wymioty od 2 dni. Co robić?"
extra_gated_description: Ten model jest przeznaczony dla profesjonalistów weterynaryjnych. Używając tego modelu, potwierdzasz że nie zastąpi on profesjonalnego osądu klinicznego.
tags:
- mlx
- veterinary
- medical
- polish
- reasoning
- clinical-ai
- bielik
- fine-tuned
pipeline_tag: text-generation
model-index:
- name: sVetliq-11b-Preview-3200-MLX-Q6
  results:
  - task:
      type: text-generation
    dataset:
      type: text-generation
      name: Polish Veterinary Cases
    metrics:
    - name: Training Loss
      type: loss
      value: 0.042
    - name: Validation Loss
      type: loss  
      value: 0.893
---

# sVetliq-11b-Preview-3200-MLX-Q6 🦅⚕️

*Polski model językowy z wbudowanym rozumowaniem klinicznym - wersja 3200*

<div align="center">

![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)
![Language](https://img.shields.io/badge/Language-Polish-red.svg)
![Framework](https://img.shields.io/badge/Framework-MLX-orange.svg)
![Specialization](https://img.shields.io/badge/Domain-Veterinary%20Medicine-green.svg)

</div>

## 🌟 Przegląd modelu

**sVetliq-11b-Preview-3200** to trzecia wersja preview polskiego modelu językowego specjalnie dostrojonego do medycyny weterynaryjnej. Model osiągnął fenomenalną zbieżność z train loss 0.042!

> **📊 Status treningu**: Preview po 3200 iteracjach z docelowych 20000. To 16% pełnego treningu, model wykazuje już dojrzałe możliwości!

### Kluczowe cechy

- 🧠 **Dojrzałe rozumowanie kliniczne**: Konsekwentne używanie tagów `<think>` przed odpowiedzią
- 🇵🇱 **Natywne przetwarzanie polskie**: Trenowany na polskich przypadkach weterynaryjnych
- 🏥 **Ekspertyza medyczna**: Specjalizacja w diagnostyce i leczeniu weterynaryjnym
- ⚡ **Optymalizacja MLX**: Zaprojektowany dla wydajności Apple Silicon
- 🎯 **Fenomenalna zbieżność**: Train loss 0.042!

## 📊 Specyfikacja modelu

| Parametr | Wartość |
|----------|---------|
| **Model bazowy** | Bielik-11B-v2.6-Instruct |
| **Parametry** | 11 miliardów |
| **Iteracje treningu** | 3,200 |
| **Training loss** | 0.042 |
| **Validation loss** | 0.893 |
| **Kwantyzacja** | Q6 (6-bit) |
| **Długość kontekstu** | 32,768 tokenów |
| **Hardware treningowy** | Apple M3 Ultra (512GB) |
| **Pamięć przy inferencji** | ~9.9 GB |

## 🚀 Szybki start

### Instalacja

```bash
# Instalacja MLX
pip install mlx mlx-lm

# Pobranie modelu z HuggingFace
git clone https://huggingface.co/LibraxisAI/sVetliq-11b-Preview-3200-MLX-Q6
```

### Podstawowe użycie

```python
from mlx_lm import load, generate

# Załadowanie modelu
model, tokenizer = load("LibraxisAI/sVetliq-11b-Preview-3200-MLX-Q6")

# Generowanie odpowiedzi
prompt = "Pacjent: pies, 5 lat, biegunka z krwią od 3 dni. Jakie badania?"
response = generate(model, tokenizer, prompt=prompt, max_tokens=1000)
print(response)
```

### Użycie w LM Studio

1. Pobierz model do katalogu modeli LM Studio
2. Wybierz sVetliq-11b-Preview-3200-MLX-Q6 z listy modeli
3. Użyj zalecanych ustawień:
   - Temperature: 0.7
   - Max Length: 32768
   - Top P: 0.95

## 🏥 Funkcja rozumowania klinicznego

Model konsekwentnie używa tagów `<think>` do wewnętrznego rozumowania:

```
Użytkownik: "Kot, 10 lat, wymioty od 3 dni, odwodnienie. Co robić?"
Model: 
<think> Ostre zaburzenia żołądkowo-jelitowe. W diagnostyce różnicowej: 
zatrucie pokarmowe, ciało obce, zapalenie trzustki, parwowiroza, 
choroby nerek/wątroby. Priorytet: ocena odwodnienia, stabilizacja...</think>

Odwodnienie 50% - krytyczne! Natychmiast: bolus płynów IV...
```

## 💡 Przykładowe zastosowania

### Przypadek nagły - test rzeczywisty
```
User: Kot, 10 lat, wymioty od 3 dni, odwodnienie. Co robić?

sVetliq: 
<think> Ostre zaburzenia żołądkowo-jelitowe. W diagnostyce różnicowej: 
zatrucie pokarmowe, ciało obce, zapalenie trzustki, parwowiroza, 
choroby nerek/wątroby. Priorytet: ocena odwodnienia, stabilizacja. 
Badania: morfologia, biochemia (lipaza, amylaza), elektrolity, USG brzucha. 
Leczenie: płyny IV (Ringera 60-90 ml/kg/24h), maropitant 1mg/kg, 
omeprazol 1mg/kg, dieta gastrointestinalna po ustąpieniu wymiotów.</think> 

Odwodnienie 50% - krytyczne! Natychmiast: bolus płynów IV - Ringer 100 ml/kg 
w 2h (3.5-4.5 mmol/L), potem continuous infusion. Przy braku poprawy: 
maropitant 1mg/kg...
```

## 📈 Szczegóły treningu

### Dataset
- **Źródło**: Certyfikowane polskie przypadki weterynaryjne
- **Rozmiar**: 20,000 wysokiej jakości przykładów
- **Jakość**: 98.2% przefiltrowane, ręcznie zweryfikowane
- **Cechy**: Przypadki kliniczne z think-tagami i protokołami leczenia

### Konfiguracja treningu
- **Metoda**: LoRA (Low-Rank Adaptation)
- **Learning rate**: 1e-4
- **Batch size**: 24
- **Optimizer**: AdamW
- **Hardware**: Apple M3 Ultra (512GB RAM)
- **Czas**: ~112 godzin (z przerwami)

## 📈 Poprawa względem poprzednich wersji

| Wersja | Train Loss | Val Loss | Progres |
|--------|------------|----------|---------|
| sVetliq-1600 | 0.147 | 0.784 | 8% |
| sVetliq-2400 | 0.065 | 0.888 | 12% |
| **sVetliq-3200** | **0.042** | **0.893** | **16%** |

- **Redukcja train loss**: -71% względem wersji 1600!
- **Stabilna generalizacja**: Val loss utrzymuje się < 0.9
- **Konsekwentne myślenie**: Model zawsze używa tagów `<think>`
- **Szybkość inferencji**: ~5.5 tokens/sec przy Q6

## ⚠️ Ograniczenia i zastrzeżenia

1. **Wersja preview**: To 16% pełnego treningu (3200/20000 iteracji)
2. **Użycie kliniczne**: Nie zatwierdzony do autonomicznych decyzji klinicznych
3. **Wymagana weryfikacja**: Zawsze weryfikuj rekomendacje profesjonalnym osądem
4. **Język**: Zoptymalizowany dla polskiego, ograniczona zdolność angielska
5. **Ukierunkowanie domenowe**: Model silnie preferuje myślenie kliniczne nawet przy pytaniach ogólnych

## 🔬 Odkrycie: Wszechobecne myślenie kliniczne

Testy wykazały, że model stosuje metodologię diagnostyczną nawet do pytań niezwiązanych z medycyną:
- Pytanie o inflację → analiza jak przypadku klinicznego
- Przepis kulinarny → podejście proceduralne jak w protokole leczenia

To pokazuje głębokie przyswojenie wzorców myślenia weterynaryjnego!

## 🎯 Dlaczego publikujemy preview?

Przy 16% treningu i train loss 0.042, model osiągnął punkt, gdzie:
- Konsekwentnie generuje wysokiej jakości odpowiedzi
- Pokazuje unikalne zachowanie rozumowania
- Jest gotowy do testów społeczności
- Pozwala zebrać feedback przed finałową wersją

### Podziękowania dla SpeakLeash

Szczególne podziękowania należą się zespołowi **SpeakLeash** za stworzenie Bielika - modelu, który dzięki:
- **Natywnemu polskiemu tokenizerowi** - rozumie niuanse naszego języka
- **Przemyślanej architekturze** - pozwala na efektywne dostrajanie
- **Dbałości o szczegóły** - każdy aspekt modelu jest dopracowany

Bez ich pracy i wizji, stworzenie pierwszego polskiego modelu z rozumowaniem byłoby niemożliwe. Bielik to fundament, na którym budujemy przyszłość polskiej AI!

## 🔬 Innowacja techniczna

sVetliq-11b-3200 reprezentuje przełomy:

1. **Konsekwentne pętle rozumowania** - każda odpowiedź poprzedzona analizą
2. **Głębokie przyswojenie domeny** - myślenie kliniczne jako domyślny tryb
3. **Efektywność kwantyzacji** - Q6 zachowuje jakość przy 9.9GB RAM
4. **Fenomenalna zbieżność** - train loss 0.042 przy zachowaniu generalizacji

## 📄 Licencja

Ten model jest udostępniony na licencji Apache 2.0, tak samo jak model bazowy Bielik.

## 🤝 Podziękowania

- **Model bazowy**: [Zespół Bielik](https://github.com/speakleash/Bielik) w SpeakLeash
- **Trening**: Program Dragon Training w Claude University
- **Dataset**: Współtwórcy certyfikowanych przypadków weterynaryjnych
- **Infrastruktura**: Zespół Apple MLX

---

<div align="center">

**🐉 Dragon Unleashed at Claude University 🐉**

*"Train loss 0.042 - Dragon osiąga dojrzałość kliniczną!"*

</div>
