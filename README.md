# PogodaStatystyka
# 📡 Statystyka Pogodowa

**Autor:** Hubert Gogola  
**Data:** Lipiec 2025  
**Opis:** Projekt pobierający i analizujący dane pogodowe ze stacji meteorologicznych IMGW w Polsce.

---

## 📦 Zawartość projektu
```python
weather-statistics/
├── app.py # Plik aplikacji (np. interfejs graficzny lub API)
├── main.py # Główne wejście – uruchamianie zbierania danych
├── data_loader.py # Wczytywanie danych z plików lub API
├── data_logger.py # Skrypt do cyklicznego logowania danych pogodowych
├── data_processing.py # Czyszczenie i przetwarzanie danych
├── visualization.py # Tworzenie wykresów i analiz graficznych
├── weather_data.csv # Dane pogodowe (surowe)
├── weather_log.csv # Plik logu danych dziennych (z historii)
├── stations_coordinates.csv # Współrzędne geograficzne stacji pogodowych
├── humidity_plot.png # Wykres wilgotności
├── temperature_plot.png # Wykres temperatury
└── pycache/ # Pliki tymczasowe Pythona
````

---

## 🔗 Źródło danych

Dane pobierane są z otwartego API Instytutu Meteorologii i Gospodarki Wodnej (IMGW):  
🔗 `https://danepubliczne.imgw.pl/api/data/synop`

---

## ⚙️ Jak to działa?

1. **`data_logger.py`** automatycznie pobiera dane pogodowe (temperatura, ciśnienie, wilgotność) i zapisuje je do pliku `weather_log.csv`.
2. **`data_processing.py`**:
   - czyści dane,
   - usuwa braki,
   - konwertuje jednostki,
   - łączy dane z lokalizacjami stacji,
   - oblicza wskaźnik odczuwalnej temperatury (**Heat Index** lub **Wind Chill**) w zależności od warunków.
3. **`visualization.py`** generuje wykresy:
   - temperatury,
   - wilgotności,
   - indeksu odczuwalnego ciepła.
4. **`main.py`** lub `app.py` mogą służyć jako interfejs do uruchamiania całej analizy lub aplikacji graficznej.

---

## 📊 Obliczenia – Heat Index i Wind Chill

- Dla temperatury powyżej 20°C liczony jest **Heat Index** (indeks ciepła).
- Dla temperatury ≤ 10°C i wiatru ≥ 4.8 km/h liczony jest **Wind Chill** (odczuwalny chłód).
- Wartość indeksu zapisywana jest jako `heat_index` w końcowej ramce danych.

---

## 💡 Przykładowe przetwarzanie danych

```python
from data_processing import preprocess_weather_data
import pandas as pd

df = pd.read_csv("weather_data.csv")
df_ready = preprocess_weather_data(df)
print(df_ready.head())
```

## 🧪 Przykładowe funkcje
pobierz_dane_pogodowe()
Pobiera aktualne dane z API IMGW i tworzy ramkę danych z kluczowymi parametrami.

zapisz_dzienne_dane()
Zapisuje dane pogodowe do dziennika weather_log.csv, łącząc nowe dane z istniejącymi.

preprocess_weather_data(df)
Kompletny pipeline:

czyszczenie danych,

łączenie z lokalizacjami,

obliczanie wskaźnika odczuwalnej temperatury.

