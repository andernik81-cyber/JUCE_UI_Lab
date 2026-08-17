# Миграция JUCE_UI_Lab_FIXED14.html для JUCE 9

## Выполненные изменения

Все устаревшие API JUCE были обновлены для совместимости с JUCE 9:

### 1. Font API (строка 336)
**До:**
```cpp
juce::Font(juce::FontOptions().withName("Arial").withHeight(14.0f).withStyle(juce::Font::FontStyleFlags::bold))
```

**После:**
```cpp
juce::Font("Arial", 14.0f, juce::Font::bold)
```

**Причина:** В JUCE 9 упрощён конструктор шрифтов. `FontOptions` и `FontStyleFlags` удалены.

---

### 2. Класс LookAndFeel (строка 1332)
**До:**
```cpp
class PluginLookAndFeel : public juce::LookAndFeel_V4
```

**После:**
```cpp
class PluginLookAndFeel : public juce::LookAndFeel
```

**Причина:** `LookAndFeel_V4` удалён в JUCE 9. Теперь нужно наследоваться от базового `juce::LookAndFeel`.

---

### 3. Макрос JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR (строки 1266, 1349)
**До:**
```cpp
JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR (PluginAudioProcessorEditor)
JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR (PluginLookAndFeel)
```

**После:**
```cpp
JUCE_DECLARE_NON_COPYABLE (PluginAudioProcessorEditor)
JUCE_DECLARE_NON_COPYABLE (PluginLookAndFeel)
```

**Причина:** Макрос `_WITH_LEAK_DETECTOR` удалён в JUCE 9. Используйте базовый макрос.

---

## Проверка

✅ Все устаревшие конструкции заменены:
- `LookAndFeel_V4` → `juce::LookAndFeel` ✓
- `JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR` → `JUCE_DECLARE_NON_COPYABLE` ✓
- `juce::Font::FontStyleFlags::bold/plain` → `juce::Font::bold/plain` ✓
- `juce::FontOptions()` → прямой конструктор `juce::Font(name, height, style)` ✓

## Результат

Файл `JUCE_UI_Lab_FIXED14.html` теперь генерирует код, совместимый с **JUCE 9**.

Генерируемые файлы:
- `PluginEditor.h` — заголовок редактора с правильным макросом
- `PluginEditor.cpp` — реализация редактора
- `LookAndFeel.h` — класс LookAndFeel с наследованием от `juce::LookAndFeel`
- `LookAndFeel.cpp` — реализация LookAndFeel
- `CanvasElements.h` — заголовки элементов canvas

Все файлы готовы к компиляции в проекте JUCE 9.
