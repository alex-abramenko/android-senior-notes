# Android Senior Roadmap

Цель: уровень синьора 2026, готовность к собеседованию в любую крупную компанию.
Срок: 12–18 месяцев при 5–8 часах в неделю.
Формат: практика через сквозной pet-проект + мини-проекты.

Отмечай чекбоксы по мере прохождения. В конце каждой фазы — короткий ретро-комментарий своими словами: что реально усвоил, что осталось мутным.

---

## Фаза 0 — Подготовка (1 неделя)

- [ ] Выбран сквозной pet-проект, описаны основные сценарии и domain-сущности
- [ ] Android Studio обновлена до последней стабильной
- [ ] JDK 17+ установлен и выбран по умолчанию
- [ ] Создан репозиторий `android-senior-notes`
- [ ] Создан репозиторий pet-проекта с пустым Android-проектом на Kotlin + Gradle Kotlin DSL
- [ ] В pet-проекте первый коммит запушен
- [ ] Этот `roadmap.md` лежит в `android-senior-notes`

---

## Фаза 1 — Kotlin в глубину (4–5 недель)

### Система типов
- [ ] `Nothing` и `Unit`: в чём разница, где используется `Nothing`
- [ ] Nullability на уровне типов, platform types при взаимодействии с Java
- [ ] Variance: `in`, `out`, `where`, use-site vs declaration-site
- [ ] `reified` и почему он работает только с `inline`
- [ ] Type erasure в JVM и как Kotlin с ним живёт
- [ ] Generic constraints, `where`-клаузы

### Классы и объекты
- [ ] `data class`: `copy`, `componentN`, `equals/hashCode`, подводные камни
- [ ] `sealed class` vs `sealed interface`, exhaustive `when`
- [ ] `value class` (inline class), boxing и его стоимость
- [ ] `object`, companion object, статика в Kotlin
- [ ] Delegation: `by` для интерфейсов, `by lazy`, `Delegates.observable`
- [ ] `open`/`final` по умолчанию, final-by-default идеология
- [ ] Видимости: `internal`, module-scope в контексте многомодульного проекта

### Функции
- [ ] `inline`, `noinline`, `crossinline` — когда что
- [ ] Higher-order functions, стоимость лямбд без `inline`
- [ ] Extension-функции: разрешение, статика, ограничения
- [ ] Scope functions: `let`/`run`/`with`/`apply`/`also` — разница и когда что
- [ ] Infix, operator overloading
- [ ] `tailrec`

### Коллекции и Sequence
- [ ] List vs MutableList, immutability в Kotlin (иллюзия vs реальность)
- [ ] Eager vs lazy: `map` на List vs на Sequence
- [ ] Когда Sequence реально выгодна, когда вредна
- [ ] `asSequence`, терминальные операции
- [ ] `groupBy`, `associate`, `fold`, `reduce`

### Обработка ошибок
- [ ] Checked vs unchecked в Kotlin, почему нет checked
- [ ] `Result<T>`, `runCatching` — плюсы и минусы
- [ ] Sealed-классы для моделирования ошибок
- [ ] `try`/`catch`/`finally` с корутинами — что ломается

### Reflection и аннотации
- [ ] `KClass` vs `Class`, `::`
- [ ] Annotation targets, `@Retention`
- [ ] Когда reflection оправдан, когда нет (стоимость)

- [ ] **Ретро по Фазе 1**

---

## Фаза 2 — Корутины и Flow (8–10 недель)

### Основы
- [ ] `suspend` как state machine, что делает компилятор
- [ ] Continuation, continuation-passing style
- [ ] `launch` vs `async`, что возвращают
- [ ] `Job` и его состояния (жизненный цикл)

### Structured concurrency
- [ ] `coroutineScope` vs `supervisorScope`
- [ ] Parent-child отношения, отмена по иерархии
- [ ] Почему `GlobalScope` — плохо
- [ ] `CoroutineScope` как поле класса, когда это правильно

### Context и диспатчеры
- [ ] `CoroutineContext` как Map, элементы контекста
- [ ] `Dispatchers.Main`/`IO`/`Default`/`Unconfined`
- [ ] `withContext`, смена диспатчера
- [ ] `CoroutineName`, `Job`, `CoroutineExceptionHandler` в контексте

### Отмена
- [ ] Кооперативная отмена, `isActive`, `ensureActive`
- [ ] `yield`
- [ ] `CancellationException` — почему её нельзя глотать
- [ ] `NonCancellable` — когда нужен
- [ ] Отмена и ресурсы: `try`/`finally`, `use`

### Исключения
- [ ] Поведение исключений в `launch` vs `async`
- [ ] `CoroutineExceptionHandler` — где работает, где нет
- [ ] `SupervisorJob` и изоляция падений
- [ ] `awaitAll`, частичные падения

### Flow
- [ ] Cold Flow: что значит "холодный"
- [ ] `flow { }`, `emit`, context preservation
- [ ] Операторы: `map`, `filter`, `transform`, `flatMapConcat/Merge/Latest`
- [ ] `flowOn`, почему менять контекст внутри `flow { }` нельзя
- [ ] `buffer`, `conflate`, `collectLatest`

### Hot Flow
- [ ] `StateFlow`: состояние, `value`, distinct-поведение
- [ ] `SharedFlow`: replay, extra buffer, `onBufferOverflow`
- [ ] `MutableStateFlow` vs `MutableSharedFlow`
- [ ] `stateIn`, `shareIn`, `SharingStarted.WhileSubscribed(5000)` — зачем 5 секунд

### Каналы
- [ ] `Channel`, типы буферов
- [ ] `produce`, `actor`
- [ ] Когда канал, а когда Flow

### Android-интеграция
- [ ] `viewModelScope`, `lifecycleScope`
- [ ] `repeatOnLifecycle`, почему не `launchWhenStarted`
- [ ] `Flow.collectAsState`/`collectAsStateWithLifecycle` (позже в Compose)
- [ ] Callback → Flow: `callbackFlow`, `awaitClose`

### Тестирование
- [ ] `kotlinx-coroutines-test`, `runTest`
- [ ] `TestDispatcher`: `StandardTestDispatcher` vs `UnconfinedTestDispatcher`
- [ ] `advanceTimeBy`, `advanceUntilIdle`
- [ ] `Turbine` для тестирования Flow

- [ ] **Ретро по Фазе 2**

---

## Фаза 3 — Android Runtime и Lifecycle (5–6 недель)

### Процессы и жизненный цикл приложения
- [ ] Android-процесс, один процесс = одна JVM
- [ ] Low Memory Killer, oom_adj, процессные приоритеты
- [ ] Что происходит при process death, как восстанавливать состояние
- [ ] `SavedStateHandle`, `onSaveInstanceState`

### Activity/Fragment lifecycle
- [ ] Полная диаграмма Activity lifecycle, включая `onSaveInstanceState`
- [ ] Configuration changes, `android:configChanges` — когда и зачем
- [ ] Fragment lifecycle, разница между жизнью фрагмента и его View
- [ ] `viewLifecycleOwner` vs `this`
- [ ] Back stack, мультитаски

### Services
- [ ] Started vs bound services
- [ ] Foreground services, типы foreground service (Android 14+)
- [ ] Ограничения на запуск из background (Android 12+)
- [ ] WorkManager — когда он вместо сервиса
- [ ] `JobScheduler` в основе

### Power management
- [ ] Doze mode, App Standby, App Standby Buckets
- [ ] Battery optimizations, whitelist
- [ ] Exact alarms (Android 12+), `SCHEDULE_EXACT_ALARM`

### Runtime
- [ ] Dalvik → ART, историческая справка
- [ ] AOT vs JIT в ART
- [ ] Baseline Profiles, Cloud Profiles
- [ ] `dex`, multidex

### ANR и Main thread
- [ ] Что такое ANR, тайминги (5 сек на ввод, fg 10 сек)
- [ ] Looper, MessageQueue, Handler — как устроен main thread
- [ ] Choreographer и 16ms/8ms бюджет

### Permissions
- [ ] Normal vs dangerous permissions
- [ ] Runtime permissions flow
- [ ] Permissions по версиям Android (storage, notifications, media)
- [ ] Scoped Storage

- [ ] **Ретро по Фазе 3**

---

## Фаза 4 — Concurrency и JMM (3–4 недели)

### Память и модель
- [ ] Java Memory Model: зачем она
- [ ] Happens-before, reordering
- [ ] `volatile`: что гарантирует, что нет
- [ ] Visibility vs atomicity — разные проблемы

### Примитивы синхронизации
- [ ] `synchronized`, monitor, biased/thin/fat lock
- [ ] `ReentrantLock`, `ReadWriteLock`
- [ ] `Atomic*`: CAS, ABA-проблема
- [ ] `CountDownLatch`, `CyclicBarrier`, `Semaphore`

### Thread pools
- [ ] `Executor`/`ExecutorService`, `ThreadPoolExecutor`
- [ ] Разные стратегии пулов, почему `Executors.newCachedThreadPool` опасен
- [ ] Fork/Join pool, work-stealing

### Concurrency bugs
- [ ] Race conditions, data races — разница
- [ ] Deadlock, livelock, starvation
- [ ] Double-checked locking и почему без volatile оно не работает

### Интеграция с корутинами
- [ ] `Mutex` из kotlinx.coroutines
- [ ] Actor pattern (хоть и deprecated)
- [ ] Когда нужен `synchronized` в корутинном коде, когда `Mutex`
- [ ] Thread-confinement как стратегия

- [ ] **Ретро по Фазе 4**

---

## Фаза 5 — Jetpack Compose (10–12 недель)

### Парадигма
- [ ] Declarative vs imperative UI
- [ ] Composable-функция как описание UI
- [ ] `@Composable` — что делает компилятор (Compose compiler plugin)
- [ ] Positional memoization

### State
- [ ] `remember`, `rememberSaveable`
- [ ] `mutableStateOf`, `MutableState`
- [ ] State hoisting
- [ ] `derivedStateOf` — когда нужен
- [ ] `snapshotFlow`

### Recomposition
- [ ] Что вызывает recomposition
- [ ] Smart recomposition, skipping
- [ ] Stability: stable vs unstable типы
- [ ] Strong skipping mode (Compose 1.7+)
- [ ] `@Stable`, `@Immutable`

### Side effects
- [ ] `LaunchedEffect`, ключи
- [ ] `DisposableEffect`
- [ ] `SideEffect`
- [ ] `rememberCoroutineScope`
- [ ] `produceState`, `rememberUpdatedState`

### Three phases
- [ ] Composition, Layout, Drawing
- [ ] Когда composition пропускается, когда layout, когда drawing
- [ ] `Modifier.layout`, кастомный layout

### Производительность
- [ ] Layout inspector, Recomposition counts
- [ ] Compose compiler metrics, стабильность классов
- [ ] `key()` в списках
- [ ] Read deferral: lambda-based modifiers

### Lists
- [ ] `LazyColumn`/`LazyRow`/`LazyVerticalGrid`
- [ ] `items(key = ...)`, stable keys
- [ ] `contentType`
- [ ] Sticky headers, animations в lazy

### Animations
- [ ] `animate*AsState`
- [ ] `Animatable`, `AnimationSpec`
- [ ] `AnimatedVisibility`, `AnimatedContent`
- [ ] Transition API
- [ ] Shared element transitions (Compose 1.7+)

### Navigation
- [ ] Navigation Compose, `NavHost`, `NavController`
- [ ] Type-safe navigation (serializable routes)
- [ ] Nested graphs, deep links
- [ ] Передача данных между экранами

### CompositionLocal
- [ ] Что это, когда использовать
- [ ] `staticCompositionLocalOf` vs `compositionLocalOf`
- [ ] Theme, `MaterialTheme`

### ViewModel-интеграция
- [ ] `hiltViewModel()`, `viewModel()`
- [ ] `collectAsStateWithLifecycle`
- [ ] UDF: state наверх, events вниз

### Interop
- [ ] `AndroidView` в Compose
- [ ] `ComposeView` в XML
- [ ] Миграционные стратегии

### Тестирование
- [ ] `createComposeRule`
- [ ] Semantics, finders, actions, assertions
- [ ] Screenshot-тесты (подробнее в Фазе 9)

- [ ] **Ретро по Фазе 5**

---

## Фаза 6 — Data layer: Retrofit, Room, DataStore (5–6 недель)

### Retrofit + OkHttp
- [ ] Retrofit: как устроен под капотом (Proxy, CallAdapter, Converter)
- [ ] `suspend` и `Flow` возвращаемые типы
- [ ] OkHttp Interceptors: application vs network
- [ ] Logging, auth, retry interceptors
- [ ] Connection pool, cache
- [ ] Certificate pinning (подробнее в Фазе 11)
- [ ] Timeouts: connect, read, write, call

### Сериализация
- [ ] kotlinx.serialization: настройка, `@Serializable`
- [ ] Polymorphism, sealed-классы в JSON
- [ ] Custom serializers
- [ ] Moshi vs kotlinx (коротко)

### Room
- [ ] Entities, DAO, Database
- [ ] `@Query`, `@Insert`, `@Update`, `@Delete`
- [ ] `Flow`-возвращающие запросы
- [ ] `@Relation`, one-to-many, many-to-many
- [ ] `@Transaction`
- [ ] Миграции, `AutoMigration`, ручные миграции
- [ ] Paging 3 + Room
- [ ] FTS4/FTS5 — когда нужно
- [ ] TypeConverters

### DataStore
- [ ] Preferences DataStore vs Proto DataStore
- [ ] Миграция с SharedPreferences
- [ ] Сериализация в Proto DataStore

### Repository
- [ ] Single Source of Truth
- [ ] NetworkBoundResource-подобные паттерны
- [ ] Кэширование стратегии
- [ ] Обработка ошибок в repository

- [ ] **Ретро по Фазе 6**

---

## Фаза 7 — Dependency Injection, Hilt (3–4 недели)

### Основы DI
- [ ] Что такое DI, зачем нужен
- [ ] Service Locator vs DI, в чём разница
- [ ] Constructor injection, field injection

### Hilt
- [ ] `@HiltAndroidApp`, `@AndroidEntryPoint`
- [ ] `@Module`, `@InstallIn`, компоненты Hilt
- [ ] Scopes: `@Singleton`, `@ActivityScoped`, `@ViewModelScoped`
- [ ] `@Provides` vs `@Binds`
- [ ] Qualifiers: `@Named`, кастомные
- [ ] Multibindings: `@IntoSet`, `@IntoMap`
- [ ] `@EntryPoint` — для не-Hilt мест
- [ ] Assisted Injection

### Мультимодульность
- [ ] Hilt в многомодульном проекте
- [ ] Где определять модули
- [ ] Component hierarchy

### Интеграции
- [ ] Hilt + ViewModel (`@HiltViewModel`)
- [ ] Hilt + WorkManager (`HiltWorker`)
- [ ] Hilt + Navigation Compose

### Тестирование
- [ ] `@HiltAndroidTest`
- [ ] `@UninstallModules`, `@BindValue`
- [ ] Test-only modules

- [ ] **Ретро по Фазе 7**

---

## Фаза 8 — Performance и профилирование (5–6 недель)

### Startup
- [ ] Cold/warm/hot start
- [ ] TTID vs TTFD
- [ ] App Startup library
- [ ] ContentProvider abuse для инициализации

### Baseline Profiles
- [ ] Как работают, что профилируют
- [ ] Macrobenchmark
- [ ] Генерация и проверка BP

### Jank
- [ ] 16ms/8ms/6ms бюджет кадра
- [ ] Choreographer, vsync
- [ ] GPU overdraw, Layout passes
- [ ] Скроллинг списков — типичные проблемы

### Memory
- [ ] Garbage collector в ART
- [ ] Heap dump, Memory Profiler
- [ ] LeakCanary — что детектит, как интегрировать
- [ ] Типичные утечки (Context, listeners, statics, inner classes)

### Трейсинг
- [ ] Perfetto: запись и чтение
- [ ] Systrace vs Perfetto
- [ ] Кастомные trace-секции (`Trace.beginSection`)

### R8/ProGuard
- [ ] Shrinking, optimization, obfuscation
- [ ] `consumer-rules.pro`, `proguard-rules.pro`
- [ ] Keep rules, что не подлежит обфускации

### APK/AAB
- [ ] APK Analyzer
- [ ] App Bundle, dynamic delivery
- [ ] Image optimization, webp, vector drawables
- [ ] Resource shrinking

### Battery и сеть
- [ ] Battery Historian
- [ ] Wakelocks, wake-up alarms
- [ ] Network batching, JobScheduler

### StrictMode
- [ ] Thread policy, VM policy
- [ ] Что ловит, как не игнорировать

- [ ] **Ретро по Фазе 8**

---

## Фаза 9 — Тестирование (4–5 недель)

### Unit-тесты
- [ ] JUnit 4 vs JUnit 5 в Android-контексте
- [ ] MockK: базовое мокирование, `every`, `verify`
- [ ] MockK: `coEvery`, `coVerify`, slots
- [ ] Относительно моков: когда мокать, когда fake
- [ ] Тест-пирамида

### Корутины в тестах
- [ ] `runTest`, time skipping
- [ ] `TestDispatcher` injection в ViewModel
- [ ] `Turbine` для Flow-тестов

### Compose-тесты
- [ ] `createComposeRule` vs `createAndroidComposeRule`
- [ ] Semantics tree
- [ ] Finders, assertions, actions

### Screenshot-тесты
- [ ] Paparazzi: как работает, ограничения
- [ ] Генерация и проверка скриншотов
- [ ] Roborazzi как альтернатива

### Hilt-тесты
- [ ] `HiltAndroidRule`
- [ ] Замена модулей в тестах

### Инструментальные тесты
- [ ] Espresso (базово, уходит в прошлое)
- [ ] UiAutomator
- [ ] Robolectric — когда оправдан

### CI
- [ ] Запуск тестов в CI
- [ ] Coverage (Kover/JaCoCo)
- [ ] Flaky tests — как с ними жить

- [ ] **Ретро по Фазе 9**

---

## Фаза 10 — Gradle, сборка, релизы (3–4 недели)

### Gradle
- [ ] Kotlin DSL vs Groovy
- [ ] Configuration vs execution phase
- [ ] Task, task dependencies
- [ ] Incremental builds, build cache, configuration cache

### Модульность сборки
- [ ] Version Catalogs (`libs.versions.toml`)
- [ ] Convention Plugins: `buildSrc` vs `build-logic`
- [ ] Composite builds

### AGP
- [ ] Build types, product flavors, variants
- [ ] Manifest merging
- [ ] Resource processing

### Release
- [ ] Signing configs, upload key vs app signing key
- [ ] Play App Signing
- [ ] Release build: R8, минификация ресурсов
- [ ] App Bundle и dynamic features

### Оптимизация сборки
- [ ] Gradle Profiler, build scan
- [ ] Параллельные сборки, `--parallel`
- [ ] KSP vs KAPT

### CI/CD
- [ ] GitHub Actions: workflow, jobs, matrix
- [ ] Кэширование Gradle в CI
- [ ] Автоматическая публикация в Play (fastlane/gradle-play-publisher)
- [ ] Автоматические PR-чеки: lint, ktlint/detekt, tests

- [ ] **Ретро по Фазе 10**

---

## Фаза 11 — Безопасность (3 недели)

### Хранение секретов
- [ ] Android Keystore: как работает, аппаратный keystore
- [ ] Key attestation
- [ ] EncryptedSharedPreferences / Jetpack Security
- [ ] Шифрование файлов

### Сеть
- [ ] Network Security Config
- [ ] Certificate Pinning (OkHttp)
- [ ] TLS-версии, cipher suites

### Аутентификация
- [ ] Biometric API, `BiometricPrompt`
- [ ] CryptoObject для подписи операций биометрией

### БД
- [ ] SQLCipher + Room
- [ ] Когда реально нужно шифровать БД

### Integrity
- [ ] Play Integrity API
- [ ] Root detection, debug detection
- [ ] Tamper detection

### Мониторинг
- [ ] Firebase Crashlytics: интеграция, кастомные ключи
- [ ] Sentry как альтернатива
- [ ] Non-fatal reports

- [ ] **Ретро по Фазе 11**

---

## Фаза 12 — Финальный pet-проект и подготовка к собеседованиям (4–6 недель)

### Pet-проект к промышленному качеству
- [ ] Все фазы интегрированы в проект
- [ ] CI/CD настроен
- [ ] Тесты покрывают критичные сценарии
- [ ] Baseline Profile сгенерирован
- [ ] Crashlytics подключён
- [ ] README с описанием архитектуры и скриншотами

### Публикация
- [ ] Google Play Console аккаунт
- [ ] Internal testing track
- [ ] Production release
- [ ] Store listing: описание, скриншоты

### Подготовка к интервью
- [ ] Резюме обновлено
- [ ] GitHub приведён в порядок (закреплён pet-проект)
- [ ] Решение задач по структурам данных и алгоритмам (базовый уровень)
- [ ] Прохождение мок-собеседований
- [ ] Реальные собеседования для калибровки

- [ ] **Финальное ретро по всему роадмапу**

---

## Контрольные точки

- [ ] Месяц 1 — обзор прогресса
- [ ] Месяц 2 — обзор прогресса
- [ ] Месяц 3 — мок-собеседование №1 (Kotlin + корутины)
- [ ] Месяц 4 — обзор прогресса
- [ ] Месяц 5 — обзор прогресса
- [ ] Месяц 6 — мок-собеседование №2 (+ Android runtime, concurrency). Реальное собеседование для калибровки.
- [ ] Месяц 7 — обзор прогресса
- [ ] Месяц 8 — обзор прогресса
- [ ] Месяц 9 — мок-собеседование №3 (+ Compose, data layer)
- [ ] Месяц 10 — обзор прогресса
- [ ] Месяц 11 — обзор прогресса
- [ ] Месяц 12 — мок-собеседование №4 (+ performance, testing). Реальные собеседования.
- [ ] Месяц 15 — итоговое мок-собеседование
- [ ] Месяц 18 — цель: оффер синьора в крупной компании
