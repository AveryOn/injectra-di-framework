# Injectra DI Framework Roadmap

## 1. Основы Dependency Injection и Inversion of Control

### 001. Исследовать Dependency Injection

Разобрать передачу зависимостей извне вместо их создания внутри dependent class.

### 002. Исследовать Inversion of Control

Определить роль container как механизма управления созданием и связыванием объектов.

### 003. Разделить Dependency Injection и Service Locator

Зафиксировать различия между явным constructor injection и скрытым получением dependencies из container.

### 004. Исследовать Constructor Injection

Разобрать преимущества обязательных зависимостей, immutable references и тестируемости.

### 005. Исследовать Property Injection

Определить ограничения optional dependencies и частично инициализированных объектов.

### 006. Исследовать Method Injection

Разобрать передачу contextual dependency только в момент вызова operation.

### 007. Исследовать Interface Injection

Рассмотреть pattern и причины его редкого использования в TypeScript.

### 008. Исследовать Composition Root

Определить единственное место сборки object graph приложения.

### 009. Исследовать Dependency Inversion Principle

Зафиксировать зависимость high-level modules от abstractions, а не concrete implementations.

### 010. Исследовать Pure DI

Собрать object graph вручную без runtime container и сравнить подходы.

### 011. Исследовать Runtime DI Container

Определить преимущества dynamic registration, scopes, modules и graph diagnostics.

### 012. Исследовать Compile-time DI

Сравнить runtime reflection с generated factories и static dependency graphs.

### 013. Исследовать Explicit DI

Разобрать регистрацию dependencies через configuration objects и factory functions.

### 014. Исследовать Decorator-based DI

Разобрать metadata-driven registration и constructor parameter resolution.

### 015. Исследовать TypeScript runtime types

Зафиксировать, какие type annotations исчезают после compilation.

### 016. Исследовать token-based resolution

Определить необходимость runtime tokens для interfaces и abstract dependencies.

### 017. Исследовать object lifecycle

Разобрать создание, кэширование, использование и disposal экземпляров.

### 018. Исследовать dependency scopes

Сравнить singleton, transient, request и custom scopes.

### 019. Исследовать dependency graph

Определить nodes, directed edges, roots, cycles и topological order.

### 020. Зафиксировать гарантии Injectra

Документировать registration semantics, resolution rules, lifecycle и error behavior framework.

## 2. Структура репозитория и базовые инструменты

### 021. Создать структуру monorepo

Разделить core framework, decorators, integrations, testing utilities, examples и benchmarks.

### 022. Создать package `@injectra/core`

Разместить container, providers, scopes, tokens и graph resolution.

### 023. Создать package `@injectra/decorators`

Разместить decorator API и metadata helpers.

### 024. Создать package `@injectra/testing`

Разместить test container, overrides, spies и graph assertions.

### 025. Создать package `@injectra/node`

Разместить Node.js-specific lifecycle и AsyncLocalStorage integrations.

### 026. Создать package `@injectra/express`

Добавить request-scope integration с Express.

### 027. Создать package `@injectra/nest-bridge`

Подготовить экспериментальную интеграцию с NestJS providers.

### 028. Создать package `@injectra/benchmarks`

Разместить startup, registration и resolution benchmarks.

### 029. Настроить TypeScript strict mode

Включить строгую проверку типов, nullability и generic constraints.

### 030. Настроить ESM

Использовать Node.js ESM и проверить package exports.

### 031. Подготовить CommonJS compatibility

Определить необходимость dual package или отдельного compatibility build.

### 032. Настроить project references

Разделить compilation packages и ускорить incremental builds.

### 033. Настроить package exports

Экспортировать только публичные API и запретить deep imports.

### 034. Настроить declaration generation

Генерировать `.d.ts` для всех public packages.

### 035. Настроить source maps

Обеспечить корректные stack traces внутри framework.

### 036. Настроить ESLint

Добавить правила для unsafe reflection, promises и public API boundaries.

### 037. Настроить Prettier

Обеспечить единое форматирование source code и documentation.

### 038. Настроить test runner

Подключить Vitest или Node.js Test Runner для unit и integration tests.

### 039. Настроить coverage

Собирать branch coverage для resolution и lifecycle paths.

### 040. Создать public API compatibility check

Обнаруживать случайные breaking changes exported types и functions.

## 3. Базовая модель token

### 041. Определить тип Token

Поддержать class constructors, symbols, strings и typed token objects.

### 042. Реализовать class token

Использовать constructor function как runtime identifier dependency.

### 043. Реализовать symbol token

Поддержать interfaces и abstractions через уникальные symbols.

### 044. Реализовать string token

Добавить compatibility mode с явным предупреждением о collision risk.

### 045. Реализовать typed InjectionToken

Создать generic token, сохраняющий compile-time тип dependency.

### 046. Добавить token description

Использовать readable description в errors и diagnostics.

### 047. Добавить token identity

Гарантировать сравнение tokens по identity, а не только по description.

### 048. Создать helper `createToken`

Упростить создание typed runtime token.

### 049. Создать helper `isToken`

Проверять допустимость значения как Injectra token.

### 050. Реализовать token serialization

Создать безопасное diagnostic representation без изменения identity.

### 051. Реализовать global token registry

Исследовать optional registry для interoperability между package copies.

### 052. Проверить duplicate package problem

Определить поведение token classes при нескольких версиях Injectra в dependency tree.

### 053. Реализовать namespaced token

Добавить namespace для library и application-level tokens.

### 054. Реализовать token aliases

Позволить нескольким tokens ссылаться на один provider.

### 055. Обнаруживать alias cycles

Запрещать A → B → A и более длинные alias loops.

### 056. Реализовать multi-token

Поддержать получение коллекции implementations для одного contract.

### 057. Определить ordering multi-providers

Зафиксировать порядок регистрации и optional priority.

### 058. Реализовать optional token wrapper

Представлять необязательную dependency без смешивания с `undefined` provider value.

### 059. Реализовать lazy token wrapper

Представлять dependency, разрешаемую при первом обращении.

### 060. Тестировать token identity

Проверить symbols, classes, strings, aliases и duplicate descriptions.

## 4. Provider model

### 061. Определить Provider union

Объединить class, value, factory, existing и multi-provider configurations.

### 062. Реализовать ClassProvider

Создавать instance указанного class constructor.

### 063. Реализовать ValueProvider

Возвращать заранее созданное значение без дополнительного lifecycle.

### 064. Реализовать FactoryProvider

Создавать dependency через user-defined factory function.

### 065. Реализовать ExistingProvider

Связывать token с другим уже зарегистрированным provider.

### 066. Реализовать ConstructorProvider

Позволить зарегистрировать class напрямую без wrapper object.

### 067. Реализовать AsyncFactoryProvider

Поддержать factory, возвращающую Promise.

### 068. Реализовать ConditionalProvider

Выбирать implementation на основании environment или configuration.

### 069. Реализовать MultiProvider

Добавлять implementation в коллекцию одного token.

### 070. Реализовать provider dependencies

Позволить factory явно объявлять список injected tokens.

### 071. Реализовать optional factory dependencies

Передавать `undefined` или default value при отсутствии optional provider.

### 072. Реализовать lazy factory dependencies

Передавать resolver function вместо готового instance.

### 073. Реализовать provider scope

Назначать singleton, transient, request или custom scope.

### 074. Реализовать eager provider flag

Создавать provider во время container bootstrap.

### 075. Реализовать provider metadata

Хранить name, source module, tags и diagnostic information.

### 076. Реализовать provider priority

Определить выбор implementation при нескольких candidate registrations.

### 077. Реализовать provider visibility

Ограничивать provider public, module-private или container-local scope.

### 078. Реализовать provider override flag

Разрешать явное замещение существующей регистрации.

### 079. Реализовать provider normalization

Преобразовывать все public provider forms в единый internal descriptor.

### 080. Тестировать provider normalization

Проверить class, value, factory, alias, async и multi registrations.

## 5. Container API

### 081. Спроектировать Container class

Определить registry, caches, scopes, parent reference и lifecycle state.

### 082. Реализовать `register`

Добавлять один или несколько providers.

### 083. Реализовать `registerMany`

Выполнять batch registration с atomic validation.

### 084. Реализовать `has`

Проверять наличие local или inherited provider.

### 085. Реализовать `resolve`

Получать synchronous dependency по token.

### 086. Реализовать `resolveAsync`

Получать dependency с поддержкой asynchronous providers.

### 087. Реализовать `resolveAll`

Получать все providers multi-token.

### 088. Реализовать `tryResolve`

Возвращать result без exception для отсутствующего optional provider.

### 089. Реализовать `create`

Создавать незарегистрированный class с разрешением его dependencies.

### 090. Реализовать `override`

Явно заменять provider в test или child container.

### 091. Реализовать `remove`

Удалять регистрацию до начала resolution lifecycle.

### 092. Реализовать `clear`

Очищать registry и caches в контролируемом состоянии.

### 093. Реализовать `freeze`

Запрещать изменение registrations после bootstrap.

### 094. Реализовать `isFrozen`

Проверять возможность последующей registration.

### 095. Реализовать `dispose`

Освобождать созданные disposable instances.

### 096. Реализовать `reset`

Очищать instances, сохраняя provider registrations.

### 097. Реализовать container state machine

Поддержать configuring, bootstrapping, ready, disposing и disposed states.

### 098. Запретить resolution после disposal

Возвращать отдельную lifecycle error.

### 099. Запретить registration после freeze

Возвращать deterministic configuration error.

### 100. Создать ContainerBuilder

Добавить fluent API для composition root без изменения runtime container API.

## 6. Dependency graph resolution

### 101. Спроектировать internal provider registry

Использовать token-indexed structure с поддержкой aliases и multi-providers.

### 102. Спроектировать resolution context

Хранить текущий path, scope, cache и diagnostic metadata.

### 103. Реализовать recursive resolution

Разрешать dependencies depth-first через provider graph.

### 104. Реализовать iterative resolution experiment

Сравнить recursive и explicit-stack algorithms.

### 105. Строить resolution path

Сохранять последовательность tokens от root до текущей dependency.

### 106. Обнаруживать отсутствующий provider

Возвращать ошибку с полным dependency path.

### 107. Обнаруживать circular dependency

Проверять повторное появление token в active resolution stack.

### 108. Формировать cycle path

Показывать `A → B → C → A` в error message.

### 109. Разделить alias cycle и constructor cycle

Возвращать разные error codes для configuration diagnostics.

### 110. Реализовать topological sort

Получать порядок eager initialization и disposal.

### 111. Обнаруживать disconnected providers

Находить registrations, недостижимые от заданных composition roots.

### 112. Обнаруживать duplicate providers

Различать accidental duplicate и intentional override.

### 113. Обнаруживать ambiguous providers

Отклонять обычный resolve при нескольких non-multi implementations.

### 114. Реализовать dependency graph snapshot

Возвращать immutable representation nodes и edges.

### 115. Реализовать graph traversal API

Позволить tools анализировать ancestors, descendants и paths.

### 116. Реализовать graph validation

Проверять missing dependencies, cycles, scopes и async boundaries без создания instances.

### 117. Реализовать dry-run resolution

Проверять object graph без вызова constructors и factories.

### 118. Реализовать root validation

Проверять только dependencies выбранных application entry points.

### 119. Реализовать full-container validation

Проверять все зарегистрированные providers.

### 120. Тестировать сложные dependency graphs

Проверить diamond graphs, aliases, multi-providers, missing nodes и cycles.

## 7. Constructor resolution

### 121. Определить Constructor type

Создать безопасный generic type для instantiable classes.

### 122. Реализовать explicit dependency list

Позволить ClassProvider задавать constructor tokens без decorators.

### 123. Реализовать static `inject` property

Поддержать class-level declaration зависимостей.

### 124. Определить precedence metadata sources

Зафиксировать порядок explicit provider deps, static inject и decorator metadata.

### 125. Реализовать constructor invocation

Создавать instance через `Reflect.construct`.

### 126. Сохранять constructor errors

Не скрывать исходный exception user class.

### 127. Оборачивать constructor errors

Добавлять token и resolution path через error cause.

### 128. Поддержать zero-argument constructors

Создавать class без metadata.

### 129. Поддержать abstract class token

Разрешать abstract constructor как token, но не как instantiable implementation.

### 130. Проверять instantiability

Обнаруживать arrow functions, plain functions и invalid constructor values.

### 131. Поддержать inherited constructor metadata

Определить наследование dependencies от base class.

### 132. Обрабатывать overridden constructor

Не смешивать metadata parent и child без явного правила.

### 133. Поддержать optional constructor dependencies

Разрешать отсутствие marked dependency.

### 134. Поддержать default constructor parameters

Определить взаимодействие optional injection и JavaScript defaults.

### 135. Поддержать rest parameters

Зафиксировать ограничения injection для variadic constructors.

### 136. Поддержать primitive dependencies

Требовать explicit tokens для string, number и boolean configuration.

### 137. Запретить неявную инъекцию `Object`

Выдавать metadata error вместо ambiguous resolution.

### 138. Запретить неявную инъекцию `Promise`

Требовать explicit async provider token.

### 139. Создать constructor dependency inspector

Возвращать tokens, optional flags и metadata source.

### 140. Тестировать constructor resolution

Проверить inheritance, optional parameters, primitives и thrown errors.

## 8. Decorators и metadata

### 141. Исследовать legacy decorators TypeScript

Разобрать `experimentalDecorators` и `emitDecoratorMetadata`.

### 142. Исследовать standard ECMAScript decorators

Сравнить новую decorator semantics с legacy implementation.

### 143. Выбрать decorator compatibility strategy

Зафиксировать поддерживаемые compiler modes.

### 144. Подключить reflect-metadata

Использовать metadata API только в decorators package.

### 145. Реализовать `@Injectable`

Помечать class как доступный для metadata-based construction.

### 146. Реализовать `@Inject`

Указывать explicit token constructor parameter.

### 147. Реализовать `@Optional`

Помечать dependency необязательной.

### 148. Реализовать `@Lazy`

Передавать lazy resolver или proxy.

### 149. Реализовать `@MultiInject`

Получать массив implementations одного multi-token.

### 150. Реализовать `@Singleton`

Назначать singleton scope class provider.

### 151. Реализовать `@Transient`

Назначать transient scope.

### 152. Реализовать `@Scoped`

Назначать built-in или custom scope.

### 153. Реализовать `@PostConstruct`

Помечать lifecycle initialization method.

### 154. Реализовать `@PreDestroy`

Помечать lifecycle disposal method.

### 155. Реализовать class registration decorator

Исследовать automatic global registration и его drawbacks.

### 156. Отделить metadata declaration от registration

Не изменять global container при import class module.

### 157. Реализовать metadata reader

Нормализовать design metadata и Injectra-specific annotations.

### 158. Проверять decorator conflicts

Отклонять одновременные несовместимые annotations.

### 159. Создать decorator-free equivalent

Документировать explicit API для каждой decorator capability.

### 160. Тестировать decorator metadata

Проверить inheritance, parameter indexes, minification и missing metadata.

## 9. Singleton и transient scopes

### 161. Реализовать singleton cache

Создавать один instance на container lifecycle.

### 162. Реализовать singleton promise cache

Не запускать async factory повторно при concurrent resolution.

### 163. Обрабатывать singleton initialization failure

Определить удаление rejected Promise из cache и возможность retry.

### 164. Защитить singleton от partial publication

Не помещать незавершённый instance в общий cache без controlled cycle strategy.

### 165. Реализовать transient scope

Создавать новый instance при каждом dependency resolution.

### 166. Проверить nested transient dependencies

Создавать независимое дерево transient instances.

### 167. Реализовать resolution-scoped instance

Переиспользовать instance только внутри одного root resolve operation.

### 168. Сравнить singleton и resolution scope

Проверить diamond dependency graph.

### 169. Реализовать scope hierarchy validation

Запрещать singleton, напрямую зависящий от request-scoped provider.

### 170. Определить transient capture policy

Предупреждать о transient dependency, сохранённой singleton instance.

### 171. Реализовать scope rank

Сравнивать lifetime provider и его dependencies.

### 172. Реализовать captive dependency detection

Находить dependency с более коротким lifecycle внутри долгоживущего provider.

### 173. Добавить strict scope mode

Отклонять captive dependencies при bootstrap validation.

### 174. Добавить warning scope mode

Публиковать diagnostic warning без остановки application.

### 175. Реализовать scope-aware aliases

Сохранять lifecycle исходного provider.

### 176. Реализовать scope-aware multi-providers

Разрешать collection из providers разных scopes с явными правилами.

### 177. Реализовать singleton reset

Удалять cached instance и корректно вызывать disposal.

### 178. Реализовать selective cache invalidation

Сбрасывать provider и зависящие от него cached instances.

### 179. Тестировать concurrent singleton resolution

Запускать множество parallel resolve одного async provider.

### 180. Тестировать scope invariants

Проверить singleton, transient, resolution scope и captive dependencies.

## 10. Request и custom scopes

### 181. Определить Scope abstraction

Создать API хранения и получения instances для конкретного lifecycle context.

### 182. Реализовать ScopeId

Использовать runtime identifier конкретного scope instance.

### 183. Реализовать request scope

Создавать один instance provider на HTTP request.

### 184. Создать child scope

Наследовать registrations root container с отдельным scoped cache.

### 185. Реализовать `runInScope`

Выполнять callback внутри созданного scope.

### 186. Реализовать scope disposal

Освобождать scoped instances после завершения callback.

### 187. Реализовать AsyncLocalStorage integration

Передавать active scope через asynchronous execution chain.

### 188. Не полагаться только на AsyncLocalStorage

Поддержать explicit scope parameter для libraries и tests.

### 189. Реализовать current scope lookup

Получать active scope с понятной ошибкой при его отсутствии.

### 190. Реализовать request context provider

Инъецировать requestId, actor и tenant context.

### 191. Запретить request scope вне request context

Возвращать отдельную MissingScopeError.

### 192. Реализовать custom scope registration

Позволить application определить lifecycle и cache strategy.

### 193. Реализовать transaction scope

Переиспользовать transaction-bound dependencies внутри unit of work.

### 194. Реализовать job scope

Создавать context на время обработки background job.

### 195. Реализовать WebSocket connection scope

Переиспользовать dependencies в lifecycle одного connection.

### 196. Реализовать manual scope

Позволить явно открывать и закрывать scope.

### 197. Реализовать nested scopes

Определить наследование caches и visibility parent scope.

### 198. Запретить scope use after disposal

Обнаруживать asynchronous work, пережившую lifecycle context.

### 199. Реализовать scope leak diagnostics

Отслеживать незакрытые scopes в development mode.

### 200. Тестировать scope propagation

Проверить promises, timers, EventEmitter, workers и concurrent requests.

## 11. Async providers и bootstrap

### 201. Определить synchronous resolution boundary

Запрещать `resolve` для graph, содержащего async provider.

### 202. Создать AsyncProviderError

Показывать token и async dependency path.

### 203. Реализовать async factory resolution

Ожидать Promise и кэшировать результат согласно scope.

### 204. Поддержать mixed sync/async graph

Разрешать sync providers внутри async root resolution.

### 205. Реализовать asynchronous class initialization

Ожидать `@PostConstruct` или lifecycle hook, возвращающий Promise.

### 206. Реализовать container bootstrap

Создавать eager providers и выполнять initialization hooks.

### 207. Вычислять bootstrap order

Инициализировать dependencies раньше dependents.

### 208. Реализовать parallel bootstrap

Параллельно создавать независимые branches graph.

### 209. Ограничить bootstrap concurrency

Не создавать чрезмерную нагрузку на database и network dependencies.

### 210. Обрабатывать bootstrap failure

Останавливать initialization и освобождать уже созданные instances.

### 211. Реализовать bootstrap rollback

Вызывать disposal в обратном порядке успешной initialization.

### 212. Реализовать bootstrap timeout

Прерывать зависший provider initialization.

### 213. Поддержать AbortSignal

Передавать cancellation в async factories и hooks.

### 214. Реализовать lazy async provider

Создавать provider только при первом `resolveAsync`.

### 215. Реализовать eager async provider

Создавать provider во время bootstrap.

### 216. Реализовать readiness state

Считать container готовым только после завершения bootstrap.

### 217. Реализовать provider health hook

Позволить initialized dependency сообщать readiness status.

### 218. Реализовать retry initialization policy

Повторять только явно retryable initialization failures.

### 219. Создать bootstrap report

Показывать duration, order и failures providers.

### 220. Тестировать asynchronous bootstrap

Проверить parallel branches, cancellation, rollback и retries.

## 12. Circular dependencies и lazy resolution

### 221. Классифицировать circular dependencies

Разделить direct, indirect, alias, module и runtime cycles.

### 222. Реализовать strict cycle detection

Отклонять constructor cycles по умолчанию.

### 223. Создать CircularDependencyError

Возвращать полный path и metadata каждого edge.

### 224. Реализовать lazy resolver

Инъецировать function `() => dependency`.

### 225. Реализовать ProviderRef

Создать typed handle для отложенного `get`.

### 226. Реализовать forward token reference

Позволить ссылаться на token, объявленный позже.

### 227. Не скрывать architectural cycles

Добавлять warning при использовании forward reference.

### 228. Реализовать lazy proxy experiment

Создавать Proxy, разрешающий target при первом property access.

### 229. Обработать methods lazy proxy

Корректно связывать `this` с resolved target.

### 230. Обработать properties lazy proxy

Передавать get, set и property descriptors.

### 231. Обработать symbols lazy proxy

Поддержать inspection, iteration и custom symbols.

### 232. Определить proxy identity semantics

Зафиксировать поведение `instanceof`, equality и reflection.

### 233. Обрабатывать async lazy dependencies

Возвращать Promise-aware ProviderRef вместо прозрачного proxy.

### 234. Реализовать cycle-breaking factory

Использовать explicit factory для позднего связывания collaborators.

### 235. Исследовать setter-based cycle resolution

Показать риск partially initialized objects.

### 236. Исследовать event-based decoupling

Разорвать dependency cycle через domain events или mediator.

### 237. Создать cycle visualization

Подсвечивать strongly connected components graph.

### 238. Реализовать Tarjan algorithm

Находить все strongly connected components container graph.

### 239. Создать cycle remediation hints

Предлагать extraction interface, mediator, lazy ref или boundary change.

### 240. Тестировать circular dependency handling

Проверить strict errors, lazy refs, proxies и module cycles.

## 13. Modules и provider visibility

### 241. Спроектировать ModuleDefinition

Добавить providers, imports, exports и metadata.

### 242. Реализовать module registration

Добавлять module providers в container registry.

### 243. Реализовать module imports

Разрешать использование exported providers других modules.

### 244. Реализовать module exports

Ограничивать доступ к internal providers.

### 245. Реализовать private providers

Не позволять resolve вне declaring module.

### 246. Реализовать global modules

Предоставлять selected exports всем modules с явной регистрацией.

### 247. Ограничить global modules

Добавить diagnostics чрезмерного global provider usage.

### 248. Реализовать dynamic modules

Создавать ModuleDefinition через configuration factory.

### 249. Реализовать async dynamic modules

Поддержать asynchronous configuration providers.

### 250. Реализовать module configuration token

Передавать typed options без global mutable state.

### 251. Реализовать module re-export

Экспортировать providers imported module.

### 252. Обнаруживать module import cycles

Возвращать отдельную ModuleCycleError.

### 253. Обнаруживать missing exports

Показывать provider, существующий в module, но не экспортированный.

### 254. Реализовать module namespaces

Предотвращать accidental token collisions между libraries.

### 255. Реализовать module instances

Определить, может ли один ModuleDefinition подключаться с разными configurations.

### 256. Поддержать multi-instance module

Изолировать providers конфигурацией и module instance ID.

### 257. Реализовать conditional module imports

Подключать integration в зависимости от environment.

### 258. Реализовать module graph snapshot

Показывать imports, exports и private providers.

### 259. Создать module validation

Проверять cycles, duplicate exports и unresolved imports.

### 260. Тестировать module boundaries

Проверить private visibility, re-exports, dynamic modules и multiple instances.

## 14. Child containers и hierarchy

### 261. Реализовать parent container

Позволить child container наследовать registrations parent.

### 262. Реализовать local provider lookup

Искать provider сначала в child, затем в parent.

### 263. Реализовать child override

Заменять parent provider только внутри child hierarchy.

### 264. Определить singleton ownership

Решить, используется ли parent singleton или создаётся child-local instance.

### 265. Реализовать inherited singleton

Переиспользовать instance container, владеющего registration.

### 266. Реализовать child-local singleton override

Создавать отдельный instance для overridden provider.

### 267. Реализовать child disposal

Не уничтожать parent-owned instances.

### 268. Реализовать hierarchy-aware scopes

Сохранять ownership cache и disposal hooks.

### 269. Реализовать container fork

Копировать registrations в независимый container snapshot.

### 270. Сравнить child и fork semantics

Документировать shared и isolated state.

### 271. Реализовать tenant child container

Изолировать tenant-specific configuration и adapters.

### 272. Реализовать plugin child container

Ограничить доступ plugin к selected host dependencies.

### 273. Реализовать test child container

Переопределять dependencies без изменения root fixture.

### 274. Ограничить parent access

Не позволять parent container разрешать child-only providers.

### 275. Реализовать hierarchy diagnostics

Показывать registration owner и resolution source.

### 276. Обнаруживать shadowed provider

Предупреждать, что child registration скрывает parent token.

### 277. Реализовать hierarchy freeze

Определить влияние freeze parent на child containers.

### 278. Реализовать hierarchy reset

Сбрасывать только owned caches выбранного container.

### 279. Тестировать nested containers

Проверить lookup, overrides, ownership и disposal на нескольких уровнях.

### 280. Документировать container hierarchy

Зафиксировать resolution, caching и lifecycle semantics.

## 15. Lifecycle hooks и disposal

### 281. Определить Disposable contract

Поддержать synchronous cleanup method.

### 282. Определить AsyncDisposable contract

Поддержать asynchronous cleanup method.

### 283. Поддержать `Symbol.dispose`

Интегрировать explicit resource management при доступности runtime.

### 284. Поддержать `Symbol.asyncDispose`

Освобождать asynchronous resources стандартным protocol.

### 285. Реализовать initialization hook

Вызывать `onInit` после создания dependencies.

### 286. Реализовать destruction hook

Вызывать `onDestroy` перед окончательным освобождением instance.

### 287. Определить lifecycle hook precedence

Зафиксировать порядок decorators, interfaces и standard symbols.

### 288. Вызывать initialization в dependency order

Инициализировать dependency раньше consuming provider.

### 289. Вызывать disposal в reverse order

Освобождать dependents раньше dependencies.

### 290. Отслеживать creation order

Сохранять точную последовательность успешно созданных instances.

### 291. Не уничтожать ValueProvider автоматически

Требовать explicit ownership flag для внешних instances.

### 292. Реализовать provider ownership

Разделить container-owned и externally-owned resources.

### 293. Реализовать disposal timeout

Не позволять одному hook бесконечно блокировать shutdown.

### 294. Передавать AbortSignal в disposal

Позволить принудительно завершить долгий cleanup.

### 295. Обрабатывать multiple disposal errors

Собирать AggregateError без прекращения cleanup остальных instances.

### 296. Сделать disposal idempotent

Не вызывать cleanup повторно для одного instance.

### 297. Реализовать partial graph disposal

Освобождать выбранный provider и container-owned dependents.

### 298. Обрабатывать reset lifecycle

Сначала уничтожать cached instances, затем разрешать повторное создание.

### 299. Интегрировать process signals

Корректно закрывать container при SIGTERM и SIGINT.

### 300. Тестировать lifecycle hooks

Проверить order, async cleanup, failures, ownership и idempotency.

## 16. Error model и diagnostics

### 301. Создать базовый InjectraError

Добавить code, message, token, path, metadata и cause.

### 302. Создать ProviderNotFoundError

Показывать missing token и dependency chain.

### 303. Создать DuplicateProviderError

Показывать conflicting registrations и source modules.

### 304. Создать AmbiguousProviderError

Показывать candidate providers и способ исправления.

### 305. Создать CircularDependencyError

Показывать cycle path.

### 306. Создать InvalidProviderError

Показывать нарушение provider schema.

### 307. Создать ScopeMismatchError

Показывать captive dependency и lifecycles.

### 308. Создать MissingScopeError

Показывать required scope и root resolution.

### 309. Создать AsyncResolutionError

Показывать async dependency внутри synchronous resolve.

### 310. Создать ContainerDisposedError

Запрещать операции над завершённым container.

### 311. Создать ContainerFrozenError

Запрещать поздние registrations.

### 312. Создать LifecycleHookError

Сохранять hook name, provider и original cause.

### 313. Создать MetadataError

Показывать отсутствующие или неоднозначные decorator metadata.

### 314. Создать ModuleVisibilityError

Показывать private provider и import/export chain.

### 315. Реализовать error formatting

Создавать краткий message и расширенный diagnostic report.

### 316. Реализовать error serialization

Возвращать безопасное JSON representation без instance values и secrets.

### 317. Добавить resolution trace

Фиксировать последовательность registry lookup, cache hit и instance creation.

### 318. Реализовать debug mode

Включать расширенную диагностику без изменения resolution semantics.

### 319. Реализовать diagnostic listeners

Публиковать registration, resolution, cache и lifecycle events.

### 320. Тестировать error stability

Зафиксировать error codes и основные diagnostic fields как public API.

## 17. Introspection и graph tooling

### 321. Реализовать provider inspection

Возвращать token, kind, scope, dependencies, module и status.

### 322. Реализовать container inspection

Показывать registrations, cached instances и active scopes.

### 323. Не раскрывать provider values

Возвращать metadata без secrets и internal object state.

### 324. Реализовать dependency graph export

Экспортировать nodes и edges в JSON.

### 325. Реализовать Graphviz DOT export

Генерировать diagram dependency graph.

### 326. Реализовать Mermaid export

Генерировать diagram для Markdown documentation.

### 327. Подсвечивать scopes в graph

Показывать singleton, transient, request и custom lifecycles.

### 328. Подсвечивать module boundaries

Группировать providers по modules.

### 329. Подсвечивать missing dependencies

Показывать unresolved graph edges.

### 330. Подсвечивать circular dependencies

Выделять strongly connected components.

### 331. Подсвечивать captive dependencies

Отмечать scope lifetime violations.

### 332. Реализовать graph diff

Сравнивать container configurations двух application versions.

### 333. Реализовать provider usage analysis

Показывать roots, consumers и resolution count.

### 334. Реализовать unused provider report

Находить registrations, не используемые выбранными roots.

### 335. Реализовать startup timeline

Показывать duration initialization каждого eager provider.

### 336. Реализовать resolution timeline

Показывать nested duration factory и constructor calls.

### 337. Реализовать cache statistics

Собирать hit, miss, create и reset counters.

### 338. Реализовать CLI `injectra inspect`

Печатать provider и module metadata.

### 339. Реализовать CLI `injectra graph`

Генерировать JSON, DOT или Mermaid graph.

### 340. Реализовать CLI `injectra validate`

Проверять registrations без запуска application.

## 18. Interceptors, hooks и extensibility

### 341. Определить ContainerPlugin interface

Позволить расширять registration, resolution и lifecycle phases.

### 342. Реализовать registration hook

Вызывать plugin при добавлении normalized provider.

### 343. Реализовать before-resolve hook

Передавать token и resolution context до lookup.

### 344. Реализовать after-resolve hook

Передавать resolved instance metadata без обязательного раскрытия value.

### 345. Реализовать before-create hook

Позволить instrumentation измерять factory или constructor invocation.

### 346. Реализовать after-create hook

Публиковать duration и provider status.

### 347. Реализовать resolution middleware

Создать controlled chain around provider creation.

### 348. Ограничить middleware mutation

Не позволять plugin незаметно изменять token identity и scope rules.

### 349. Реализовать provider transformer

Позволить build-time или bootstrap-time transformation descriptor.

### 350. Реализовать instance decorator

Оборачивать instance через explicit provider configuration.

### 351. Исследовать method interception

Создать optional Proxy-based AOP experiment.

### 352. Реализовать logging interceptor example

Логировать method duration без изменения business class.

### 353. Реализовать transaction interceptor example

Открывать transaction вокруг annotated application method.

### 354. Зафиксировать ограничения AOP

Документировать private fields, identity, stack traces и performance overhead.

### 355. Реализовать plugin ordering

Использовать priority и deterministic sequence.

### 356. Реализовать plugin isolation

Не позволять failure необязательного diagnostic plugin разрушать resolution.

### 357. Реализовать critical plugin mode

Останавливать container при failure security или validation plugin.

### 358. Реализовать plugin disposal

Освобождать resources extensions вместе с container.

### 359. Создать OpenTelemetry plugin

Трассировать provider resolution и initialization.

### 360. Тестировать plugin API

Проверить ordering, errors, async hooks и disposal.

## 19. Testing utilities

### 361. Создать TestContainer

Добавить упрощённую configuration и automatic cleanup.

### 362. Реализовать provider override

Заменять production dependency test double.

### 363. Реализовать value stub

Регистрировать plain object как typed test dependency.

### 364. Реализовать factory spy

Отслеживать количество и порядок provider creation.

### 365. Реализовать constructor spy

Проверять lifecycle без изменения production class.

### 366. Реализовать resolution assertions

Проверять, что token разрешается ожидаемым implementation.

### 367. Реализовать scope assertions

Проверять equality instances между resolutions и scopes.

### 368. Реализовать dependency assertions

Проверять direct и transitive graph edges.

### 369. Реализовать no-cycle assertion

Проверять отсутствие circular dependencies.

### 370. Реализовать no-captive-dependency assertion

Проверять lifecycle compatibility.

### 371. Реализовать module-boundary assertion

Проверять imports, exports и private providers.

### 372. Реализовать disposal assertions

Проверять вызовы cleanup hooks.

### 373. Реализовать snapshot graph testing

Сравнивать dependency graph с зафиксированным snapshot.

### 374. Реализовать isolated scope helper

Автоматически создавать и закрывать request или job scope.

### 375. Реализовать fake clock provider

Тестировать lifecycle timeout и expiration.

### 376. Реализовать fake configuration provider

Передавать deterministic environment values.

### 377. Реализовать auto-mock experiment

Генерировать basic mocks для отсутствующих dependencies.

### 378. Ограничить auto-mocking

Не скрывать missing critical providers по умолчанию.

### 379. Реализовать test leak detection

Проверять незакрытые scopes и undisposed instances после test.

### 380. Документировать testing patterns

Показать unit tests без container и integration tests с TestContainer.

## 20. Полный test suite и корректность

### 381. Создать tests token model

Проверить identity, aliases, optional, lazy и multi-tokens.

### 382. Создать tests provider registration

Проверить все provider kinds, overrides и invalid descriptors.

### 383. Создать tests synchronous resolution

Проверить class, value, factory и alias graphs.

### 384. Создать tests asynchronous resolution

Проверить async factories, concurrent calls и rejected initialization.

### 385. Создать tests singleton scope

Проверить единичное создание и cache reset.

### 386. Создать tests transient scope

Проверить новое дерево instances при каждом resolution.

### 387. Создать tests request scope

Проверить reuse внутри scope и isolation между scopes.

### 388. Создать tests resolution scope

Проверить diamond dependency graph.

### 389. Создать tests custom scopes

Проверить user-defined cache и disposal strategy.

### 390. Создать tests circular dependencies

Проверить direct, indirect, alias и module cycles.

### 391. Создать tests decorator API

Проверить metadata, inheritance и explicit token overrides.

### 392. Создать tests module system

Проверить imports, exports, private providers и dynamic configuration.

### 393. Создать tests child containers

Проверить overrides, singleton ownership и hierarchy disposal.

### 394. Создать tests lifecycle

Проверить initialization, rollback, disposal и AggregateError.

### 395. Создать tests graph validation

Проверить missing providers, ambiguity и captive dependencies.

### 396. Создать concurrency tests

Выполнять parallel resolution singleton, async и scoped providers.

### 397. Создать fuzz tests provider graphs

Генерировать случайные acyclic и cyclic dependency graphs.

### 398. Создать property-based tests

Проверять invariants caching, disposal order и graph resolution.

### 399. Создать memory leak tests

Проверять освобождение transient graphs и disposed scopes через WeakRef.

### 400. Создать compatibility tests

Проверить поддерживаемые Node.js и TypeScript versions.

## 21. Performance, integrations и production-style сценарии

### 401. Определить performance targets

Зафиксировать registration time, bootstrap time, resolve latency и memory overhead.

### 402. Создать direct construction baseline

Сравнить container resolution с ручным `new`.

### 403. Создать singleton resolution benchmark

Измерить cached lookup по class, symbol и InjectionToken.

### 404. Создать transient graph benchmark

Измерить создание глубокого object graph.

### 405. Создать decorator metadata benchmark

Сравнить reflection-based и explicit dependency resolution.

### 406. Создать async provider benchmark

Измерить concurrent singleton initialization.

### 407. Создать request scope benchmark

Измерить создание и disposal scope на HTTP request.

### 408. Создать large graph benchmark

Проверить validation и bootstrap тысяч providers.

### 409. Оптимизировать registry lookup

Сравнить Map structures, normalized descriptors и alias indirection.

### 410. Оптимизировать metadata cache

Не выполнять повторное reflection чтение constructor dependencies.

### 411. Оптимизировать graph validation

Кэшировать validated graph до изменения registrations.

### 412. Оптимизировать error path allocation

Не создавать тяжёлые diagnostic objects при успешном resolution.

### 413. Реализовать Express integration

Создавать request scope middleware и освобождать его после response.

### 414. Реализовать HTTP server example

Собрать controller, service, repository, logger и request context через Injectra.

### 415. Реализовать worker application example

Создавать job scope для каждого background task.

### 416. Реализовать Hexagonal Architecture example

Связать application ports с PostgreSQL, Redis и messaging adapters.

### 417. Реализовать module replacement scenario

Переключать in-memory и production adapters без изменения application layer.

### 418. Реализовать production shutdown scenario

Корректно завершать HTTP server, database pool, Redis и message consumers.

### 419. Создать architecture documentation

Добавить C4 diagrams, dependency graph, lifecycle diagrams, ADR и public API reference.

### 420. Подготовить production readiness checklist

Зафиксировать требования к API stability, scopes, async initialization, diagnostics, performance, testing, compatibility и lifecycle safety.
