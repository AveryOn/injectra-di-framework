# Injectra DI Framework Roadmap

## 1. Dependency Injection and Inversion of Control Fundamentals

### 001. Research Dependency Injection

Examine passing dependencies from the outside instead of creating them inside the dependent class.

### 002. Research Inversion of Control

Define the role of the container as a mechanism for managing object creation and wiring.

### 003. Separate Dependency Injection and Service Locator

Record the differences between explicit constructor injection and hidden retrieval of dependencies from the container.

### 004. Research Constructor Injection

Examine the advantages of required dependencies, immutable references, and testability.

### 005. Research Property Injection

Define the limitations of optional dependencies and partially initialized objects.

### 006. Research Method Injection

Examine passing a contextual dependency only at the moment an operation is called.

### 007. Research Interface Injection

Consider the pattern and the reasons for its rare use in TypeScript.

### 008. Research Composition Root

Define the single place where the application's object graph is assembled.

### 009. Research Dependency Inversion Principle

Record the dependency of high-level modules on abstractions rather than concrete implementations.

### 010. Research Pure DI

Assemble the object graph manually without a runtime container and compare the approaches.

### 011. Research Runtime DI Container

Define the advantages of dynamic registration, scopes, modules, and graph diagnostics.

### 012. Research Compile-time DI

Compare runtime reflection with generated factories and static dependency graphs.

### 013. Research Explicit DI

Examine dependency registration through configuration objects and factory functions.

### 014. Research Decorator-based DI

Examine metadata-driven registration and constructor parameter resolution.

### 015. Research TypeScript Runtime Types

Record which type annotations disappear after compilation.

### 016. Research Token-based Resolution

Define the need for runtime tokens for interfaces and abstract dependencies.

### 017. Research Object Lifecycle

Examine instance creation, caching, use, and disposal.

### 018. Research Dependency Scopes

Compare singleton, transient, request, and custom scopes.

### 019. Research Dependency Graph

Define nodes, directed edges, roots, cycles, and topological order.

### 020. Record Injectra Guarantees

Document the framework's registration semantics, resolution rules, lifecycle, and error behavior.

## 2. Repository Structure and Core Tooling

### 021. Create Monorepo Structure

Separate the core framework, decorators, integrations, testing utilities, examples, and benchmarks.

### 022. Create Package `@injectra/core`

Place the container, providers, scopes, tokens, and graph resolution there.

### 023. Create Package `@injectra/decorators`

Place the decorator API and metadata helpers there.

### 024. Create Package `@injectra/testing`

Place the test container, overrides, spies, and graph assertions there.

### 025. Create Package `@injectra/node`

Place Node.js-specific lifecycle and AsyncLocalStorage integrations there.

### 026. Create Package `@injectra/express`

Add request-scope integration with Express.

### 027. Create Package `@injectra/nest-bridge`

Prepare an experimental integration with NestJS providers.

### 028. Create Package `@injectra/benchmarks`

Place startup, registration, and resolution benchmarks there.

### 029. Configure TypeScript Strict Mode

Enable strict type checking, nullability, and generic constraints.

### 030. Configure ESM

Use Node.js ESM and verify package exports.

### 031. Prepare CommonJS Compatibility

Determine the need for a dual package or a separate compatibility build.

### 032. Configure Project References

Separate package compilation and accelerate incremental builds.

### 033. Configure Package Exports

Export only public APIs and prohibit deep imports.

### 034. Configure Declaration Generation

Generate `.d.ts` files for all public packages.

### 035. Configure Source Maps

Ensure correct stack traces inside the framework.

### 036. Configure ESLint

Add rules for unsafe reflection, promises, and public API boundaries.

### 037. Configure Prettier

Ensure consistent formatting of source code and documentation.

### 038. Configure Test Runner

Connect Vitest or Node.js Test Runner for unit and integration tests.

### 039. Configure Coverage

Collect branch coverage for resolution and lifecycle paths.

### 040. Create Public API Compatibility Check

Detect accidental breaking changes in exported types and functions.

## 3. Basic Token Model

### 041. Define Token Type

Support class constructors, symbols, strings, and typed token objects.

### 042. Implement Class Token

Use a constructor function as a runtime dependency identifier.

### 043. Implement Symbol Token

Support interfaces and abstractions through unique symbols.

### 044. Implement String Token

Add a compatibility mode with an explicit warning about collision risk.

### 045. Implement Typed InjectionToken

Create a generic token that preserves the dependency's compile-time type.

### 046. Add Token Description

Use a readable description in errors and diagnostics.

### 047. Add Token Identity

Guarantee token comparison by identity, not only by description.

### 048. Create Helper `createToken`

Simplify creation of a typed runtime token.

### 049. Create Helper `isToken`

Check whether a value is valid as an Injectra token.

### 050. Implement Token Serialization

Create a safe diagnostic representation without changing identity.

### 051. Implement Global Token Registry

Research an optional registry for interoperability between package copies.

### 052. Check Duplicate Package Problem

Define the behavior of token classes when multiple Injectra versions exist in the dependency tree.

### 053. Implement Namespaced Token

Add a namespace for library-level and application-level tokens.

### 054. Implement Token Aliases

Allow multiple tokens to reference one provider.

### 055. Detect Alias Cycles

Prohibit A → B → A and longer alias loops.

### 056. Implement Multi-token

Support obtaining a collection of implementations for one contract.

### 057. Define Multi-provider Ordering

Record registration order and optional priority.

### 058. Implement Optional Token Wrapper

Represent an optional dependency without mixing it with an `undefined` provider value.

### 059. Implement Lazy Token Wrapper

Represent a dependency resolved on first access.

### 060. Test Token Identity

Verify symbols, classes, strings, aliases, and duplicate descriptions.

## 4. Provider Model

### 061. Define Provider Union

Combine class, value, factory, existing, and multi-provider configurations.

### 062. Implement ClassProvider

Create an instance of the specified class constructor.

### 063. Implement ValueProvider

Return a pre-created value without an additional lifecycle.

### 064. Implement FactoryProvider

Create a dependency through a user-defined factory function.

### 065. Implement ExistingProvider

Bind a token to another already registered provider.

### 066. Implement ConstructorProvider

Allow a class to be registered directly without a wrapper object.

### 067. Implement AsyncFactoryProvider

Support a factory that returns a Promise.

### 068. Implement ConditionalProvider

Select an implementation based on environment or configuration.

### 069. Implement MultiProvider

Add an implementation to the collection of one token.

### 070. Implement Provider Dependencies

Allow a factory to explicitly declare a list of injected tokens.

### 071. Implement Optional Factory Dependencies

Pass `undefined` or a default value when an optional provider is absent.

### 072. Implement Lazy Factory Dependencies

Pass a resolver function instead of a ready instance.

### 073. Implement Provider Scope

Assign singleton, transient, request, or custom scope.

### 074. Implement Eager Provider Flag

Create the provider during container bootstrap.

### 075. Implement Provider Metadata

Store name, source module, tags, and diagnostic information.

### 076. Implement Provider Priority

Define implementation selection when multiple candidate registrations exist.

### 077. Implement Provider Visibility

Limit the provider to public, module-private, or container-local scope.

### 078. Implement Provider Override Flag

Allow explicit replacement of an existing registration.

### 079. Implement Provider Normalization

Transform all public provider forms into a single internal descriptor.

### 080. Test Provider Normalization

Verify class, value, factory, alias, async, and multi registrations.

## 5. Container API

### 081. Design Container Class

Define registry, caches, scopes, parent reference, and lifecycle state.

### 082. Implement `register`

Add one or more providers.

### 083. Implement `registerMany`

Perform batch registration with atomic validation.

### 084. Implement `has`

Check for a local or inherited provider.

### 085. Implement `resolve`

Obtain a synchronous dependency by token.

### 086. Implement `resolveAsync`

Obtain a dependency with support for asynchronous providers.

### 087. Implement `resolveAll`

Obtain all providers of a multi-token.

### 088. Implement `tryResolve`

Return a result without an exception for a missing optional provider.

### 089. Implement `create`

Create an unregistered class with resolution of its dependencies.

### 090. Implement `override`

Explicitly replace a provider in a test or child container.

### 091. Implement `remove`

Remove a registration before the resolution lifecycle begins.

### 092. Implement `clear`

Clear the registry and caches in a controlled state.

### 093. Implement `freeze`

Prohibit changing registrations after bootstrap.

### 094. Implement `isFrozen`

Check whether subsequent registration is possible.

### 095. Implement `dispose`

Release created disposable instances.

### 096. Implement `reset`

Clear instances while preserving provider registrations.

### 097. Implement Container State Machine

Support configuring, bootstrapping, ready, disposing, and disposed states.

### 098. Prohibit Resolution After Disposal

Return a separate lifecycle error.

### 099. Prohibit Registration After Freeze

Return a deterministic configuration error.

### 100. Create ContainerBuilder

Add a fluent API for the composition root without changing the runtime container API.

## 6. Dependency Graph Resolution

### 101. Design Internal Provider Registry

Use a token-indexed structure with support for aliases and multi-providers.

### 102. Design Resolution Context

Store the current path, scope, cache, and diagnostic metadata.

### 103. Implement Recursive Resolution

Resolve dependencies depth-first through the provider graph.

### 104. Implement Iterative Resolution Experiment

Compare recursive and explicit-stack algorithms.

### 105. Build Resolution Path

Store the sequence of tokens from the root to the current dependency.

### 106. Detect Missing Provider

Return an error with the full dependency path.

### 107. Detect Circular Dependency

Check for the repeated appearance of a token in the active resolution stack.

### 108. Build Cycle Path

Show `A → B → C → A` in the error message.

### 109. Separate Alias Cycle and Constructor Cycle

Return different error codes for configuration diagnostics.

### 110. Implement Topological Sort

Obtain the order of eager initialization and disposal.

### 111. Detect Disconnected Providers

Find registrations unreachable from the specified composition roots.

### 112. Detect Duplicate Providers

Distinguish an accidental duplicate from an intentional override.

### 113. Detect Ambiguous Providers

Reject a regular resolve when multiple non-multi implementations exist.

### 114. Implement Dependency Graph Snapshot

Return an immutable representation of nodes and edges.

### 115. Implement Graph Traversal API

Allow tools to analyze ancestors, descendants, and paths.

### 116. Implement Graph Validation

Check missing dependencies, cycles, scopes, and async boundaries without creating instances.

### 117. Implement Dry-run Resolution

Check the object graph without invoking constructors and factories.

### 118. Implement Root Validation

Check only the dependencies of selected application entry points.

### 119. Implement Full-container Validation

Check all registered providers.

### 120. Test Complex Dependency Graphs

Verify diamond graphs, aliases, multi-providers, missing nodes, and cycles.

## 7. Constructor Resolution

### 121. Define Constructor Type

Create a safe generic type for instantiable classes.

### 122. Implement Explicit Dependency List

Allow ClassProvider to specify constructor tokens without decorators.

### 123. Implement Static `inject` Property

Support class-level dependency declaration.

### 124. Define Metadata Source Precedence

Record the order of explicit provider deps, static inject, and decorator metadata.

### 125. Implement Constructor Invocation

Create an instance through `Reflect.construct`.

### 126. Preserve Constructor Errors

Do not hide the original exception from the user class.

### 127. Wrap Constructor Errors

Add the token and resolution path through the error cause.

### 128. Support Zero-argument Constructors

Create a class without metadata.

### 129. Support Abstract Class Token

Resolve an abstract constructor as a token, but not as an instantiable implementation.

### 130. Check Instantiability

Detect arrow functions, plain functions, and invalid constructor values.

### 131. Support Inherited Constructor Metadata

Define inheritance of dependencies from the base class.

### 132. Handle Overridden Constructor

Do not mix parent and child metadata without an explicit rule.

### 133. Support Optional Constructor Dependencies

Allow a marked dependency to be absent.

### 134. Support Default Constructor Parameters

Define the interaction between optional injection and JavaScript defaults.

### 135. Support Rest Parameters

Record injection limitations for variadic constructors.

### 136. Support Primitive Dependencies

Require explicit tokens for string, number, and boolean configuration.

### 137. Prohibit Implicit Injection of `Object`

Return a metadata error instead of ambiguous resolution.

### 138. Prohibit Implicit Injection of `Promise`

Require an explicit async provider token.

### 139. Create Constructor Dependency Inspector

Return tokens, optional flags, and metadata source.

### 140. Test Constructor Resolution

Verify inheritance, optional parameters, primitives, and thrown errors.

## 8. Decorators and Metadata

### 141. Research TypeScript Legacy Decorators

Examine `experimentalDecorators` and `emitDecoratorMetadata`.

### 142. Research Standard ECMAScript Decorators

Compare the new decorator semantics with the legacy implementation.

### 143. Choose Decorator Compatibility Strategy

Record the supported compiler modes.

### 144. Connect reflect-metadata

Use the metadata API only in the decorators package.

### 145. Implement `@Injectable`

Mark a class as available for metadata-based construction.

### 146. Implement `@Inject`

Specify an explicit token for a constructor parameter.

### 147. Implement `@Optional`

Mark a dependency as optional.

### 148. Implement `@Lazy`

Pass a lazy resolver or proxy.

### 149. Implement `@MultiInject`

Obtain an array of implementations for one multi-token.

### 150. Implement `@Singleton`

Assign singleton scope to a class provider.

### 151. Implement `@Transient`

Assign transient scope.

### 152. Implement `@Scoped`

Assign a built-in or custom scope.

### 153. Implement `@PostConstruct`

Mark a lifecycle initialization method.

### 154. Implement `@PreDestroy`

Mark a lifecycle disposal method.

### 155. Implement Class Registration Decorator

Research automatic global registration and its drawbacks.

### 156. Separate Metadata Declaration from Registration

Do not modify the global container when importing a class module.

### 157. Implement Metadata Reader

Normalize design metadata and Injectra-specific annotations.

### 158. Check Decorator Conflicts

Reject simultaneous incompatible annotations.

### 159. Create Decorator-free Equivalent

Document an explicit API for each decorator capability.

### 160. Test Decorator Metadata

Verify inheritance, parameter indexes, minification, and missing metadata.

## 9. Singleton and Transient Scopes

### 161. Implement Singleton Cache

Create one instance per container lifecycle.

### 162. Implement Singleton Promise Cache

Do not start an async factory repeatedly during concurrent resolution.

### 163. Handle Singleton Initialization Failure

Define removal of a rejected Promise from the cache and the possibility of retry.

### 164. Protect Singleton from Partial Publication

Do not place an unfinished instance in the shared cache without a controlled cycle strategy.

### 165. Implement Transient Scope

Create a new instance on every dependency resolution.

### 166. Check Nested Transient Dependencies

Create an independent tree of transient instances.

### 167. Implement Resolution-scoped Instance

Reuse an instance only within one root resolve operation.

### 168. Compare Singleton and Resolution Scope

Check a diamond dependency graph.

### 169. Implement Scope Hierarchy Validation

Prohibit a singleton from directly depending on a request-scoped provider.

### 170. Define Transient Capture Policy

Warn about a transient dependency stored by a singleton instance.

### 171. Implement Scope Rank

Compare the lifetime of a provider and its dependencies.

### 172. Implement Captive Dependency Detection

Find a dependency with a shorter lifecycle inside a long-lived provider.

### 173. Add Strict Scope Mode

Reject captive dependencies during bootstrap validation.

### 174. Add Warning Scope Mode

Publish a diagnostic warning without stopping the application.

### 175. Implement Scope-aware Aliases

Preserve the lifecycle of the original provider.

### 176. Implement Scope-aware Multi-providers

Allow a collection of providers with different scopes under explicit rules.

### 177. Implement Singleton Reset

Remove the cached instance and correctly invoke disposal.

### 178. Implement Selective Cache Invalidation

Reset a provider and cached instances that depend on it.

### 179. Test Concurrent Singleton Resolution

Run many parallel resolves of one async provider.

### 180. Test Scope Invariants

Verify singleton, transient, resolution scope, and captive dependencies.

## 10. Request and Custom Scopes

### 181. Define Scope Abstraction

Create an API for storing and obtaining instances for a specific lifecycle context.

### 182. Implement ScopeId

Use a runtime identifier of a specific scope instance.

### 183. Implement Request Scope

Create one provider instance per HTTP request.

### 184. Create Child Scope

Inherit root container registrations with a separate scoped cache.

### 185. Implement `runInScope`

Execute a callback inside a created scope.

### 186. Implement Scope Disposal

Release scoped instances after the callback finishes.

### 187. Implement AsyncLocalStorage Integration

Propagate the active scope through the asynchronous execution chain.

### 188. Do Not Rely Only on AsyncLocalStorage

Support an explicit scope parameter for libraries and tests.

### 189. Implement Current Scope Lookup

Obtain the active scope with a clear error when it is absent.

### 190. Implement Request Context Provider

Inject requestId, actor, and tenant context.

### 191. Prohibit Request Scope Outside Request Context

Return a separate MissingScopeError.

### 192. Implement Custom Scope Registration

Allow the application to define lifecycle and cache strategy.

### 193. Implement Transaction Scope

Reuse transaction-bound dependencies inside a unit of work.

### 194. Implement Job Scope

Create a context for the duration of background job processing.

### 195. Implement WebSocket Connection Scope

Reuse dependencies in the lifecycle of one connection.

### 196. Implement Manual Scope

Allow explicitly opening and closing a scope.

### 197. Implement Nested Scopes

Define cache inheritance and parent-scope visibility.

### 198. Prohibit Scope Use After Disposal

Detect asynchronous work that outlives the lifecycle context.

### 199. Implement Scope Leak Diagnostics

Track unclosed scopes in development mode.

### 200. Test Scope Propagation

Verify promises, timers, EventEmitter, workers, and concurrent requests.

## 11. Async Providers and Bootstrap

### 201. Define Synchronous Resolution Boundary

Prohibit `resolve` for a graph containing an async provider.

### 202. Create AsyncProviderError

Show the token and async dependency path.

### 203. Implement Async Factory Resolution

Await the Promise and cache the result according to scope.

### 204. Support Mixed Sync/Async Graph

Allow sync providers inside async root resolution.

### 205. Implement Asynchronous Class Initialization

Await `@PostConstruct` or a lifecycle hook that returns a Promise.

### 206. Implement Container Bootstrap

Create eager providers and execute initialization hooks.

### 207. Calculate Bootstrap Order

Initialize dependencies before dependents.

### 208. Implement Parallel Bootstrap

Create independent graph branches in parallel.

### 209. Limit Bootstrap Concurrency

Do not create excessive load on database and network dependencies.

### 210. Handle Bootstrap Failure

Stop initialization and release already created instances.

### 211. Implement Bootstrap Rollback

Invoke disposal in reverse order of successful initialization.

### 212. Implement Bootstrap Timeout

Interrupt a hung provider initialization.

### 213. Support AbortSignal

Pass cancellation to async factories and hooks.

### 214. Implement Lazy Async Provider

Create the provider only on the first `resolveAsync`.

### 215. Implement Eager Async Provider

Create the provider during bootstrap.

### 216. Implement Readiness State

Consider the container ready only after bootstrap completes.

### 217. Implement Provider Health Hook

Allow an initialized dependency to report readiness status.

### 218. Implement Retry Initialization Policy

Retry only explicitly retryable initialization failures.

### 219. Create Bootstrap Report

Show provider duration, order, and failures.

### 220. Test Asynchronous Bootstrap

Verify parallel branches, cancellation, rollback, and retries.

## 12. Circular Dependencies and Lazy Resolution

### 221. Classify Circular Dependencies

Separate direct, indirect, alias, module, and runtime cycles.

### 222. Implement Strict Cycle Detection

Reject constructor cycles by default.

### 223. Create CircularDependencyError

Return the full path and metadata of each edge.

### 224. Implement Lazy Resolver

Inject a function `() => dependency`.

### 225. Implement ProviderRef

Create a typed handle for deferred `get`.

### 226. Implement Forward Token Reference

Allow referencing a token declared later.

### 227. Do Not Hide Architectural Cycles

Add a warning when a forward reference is used.

### 228. Implement Lazy Proxy Experiment

Create a Proxy that resolves the target on first property access.

### 229. Handle Lazy Proxy Methods

Correctly bind `this` to the resolved target.

### 230. Handle Lazy Proxy Properties

Forward get, set, and property descriptors.

### 231. Handle Lazy Proxy Symbols

Support inspection, iteration, and custom symbols.

### 232. Define Proxy Identity Semantics

Record the behavior of `instanceof`, equality, and reflection.

### 233. Handle Async Lazy Dependencies

Return a Promise-aware ProviderRef instead of a transparent proxy.

### 234. Implement Cycle-breaking Factory

Use an explicit factory for late binding of collaborators.

### 235. Research Setter-based Cycle Resolution

Show the risk of partially initialized objects.

### 236. Research Event-based Decoupling

Break the dependency cycle through domain events or a mediator.

### 237. Create Cycle Visualization

Highlight strongly connected components of the graph.

### 238. Implement Tarjan Algorithm

Find all strongly connected components of the container graph.

### 239. Create Cycle Remediation Hints

Suggest interface extraction, mediator, lazy ref, or boundary change.

### 240. Test Circular Dependency Handling

Verify strict errors, lazy refs, proxies, and module cycles.

## 13. Modules and Provider Visibility

### 241. Design ModuleDefinition

Add providers, imports, exports, and metadata.

### 242. Implement Module Registration

Add module providers to the container registry.

### 243. Implement Module Imports

Allow use of exported providers from other modules.

### 244. Implement Module Exports

Limit access to internal providers.

### 245. Implement Private Providers

Do not allow resolve outside the declaring module.

### 246. Implement Global Modules

Provide selected exports to all modules with explicit registration.

### 247. Limit Global Modules

Add diagnostics for excessive use of global providers.

### 248. Implement Dynamic Modules

Create ModuleDefinition through a configuration factory.

### 249. Implement Async Dynamic Modules

Support asynchronous configuration providers.

### 250. Implement Module Configuration Token

Pass typed options without global mutable state.

### 251. Implement Module Re-export

Export providers from an imported module.

### 252. Detect Module Import Cycles

Return a separate ModuleCycleError.

### 253. Detect Missing Exports

Show a provider that exists in a module but is not exported.

### 254. Implement Module Namespaces

Prevent accidental token collisions between libraries.

### 255. Implement Module Instances

Define whether one ModuleDefinition can be connected with different configurations.

### 256. Support Multi-instance Module

Isolate providers by configuration and module instance ID.

### 257. Implement Conditional Module Imports

Connect an integration depending on the environment.

### 258. Implement Module Graph Snapshot

Show imports, exports, and private providers.

### 259. Create Module Validation

Check cycles, duplicate exports, and unresolved imports.

### 260. Test Module Boundaries

Verify private visibility, re-exports, dynamic modules, and multiple instances.

## 14. Child Containers and Hierarchy

### 261. Implement Parent Container

Allow a child container to inherit parent registrations.

### 262. Implement Local Provider Lookup

Search for a provider first in the child, then in the parent.

### 263. Implement Child Override

Replace a parent provider only inside the child hierarchy.

### 264. Define Singleton Ownership

Decide whether the parent singleton is used or a child-local instance is created.

### 265. Implement Inherited Singleton

Reuse the instance of the container that owns the registration.

### 266. Implement Child-local Singleton Override

Create a separate instance for an overridden provider.

### 267. Implement Child Disposal

Do not destroy parent-owned instances.

### 268. Implement Hierarchy-aware Scopes

Preserve cache ownership and disposal hooks.

### 269. Implement Container Fork

Copy registrations into an independent container snapshot.

### 270. Compare Child and Fork Semantics

Document shared and isolated state.

### 271. Implement Tenant Child Container

Isolate tenant-specific configuration and adapters.

### 272. Implement Plugin Child Container

Limit plugin access to selected host dependencies.

### 273. Implement Test Child Container

Override dependencies without changing the root fixture.

### 274. Limit Parent Access

Do not allow the parent container to resolve child-only providers.

### 275. Implement Hierarchy Diagnostics

Show registration owner and resolution source.

### 276. Detect Shadowed Provider

Warn that a child registration hides a parent token.

### 277. Implement Hierarchy Freeze

Define the effect of freezing the parent on child containers.

### 278. Implement Hierarchy Reset

Reset only caches owned by the selected container.

### 279. Test Nested Containers

Verify lookup, overrides, ownership, and disposal across multiple levels.

### 280. Document Container Hierarchy

Record resolution, caching, and lifecycle semantics.

## 15. Lifecycle Hooks and Disposal

### 281. Define Disposable Contract

Support a synchronous cleanup method.

### 282. Define AsyncDisposable Contract

Support an asynchronous cleanup method.

### 283. Support `Symbol.dispose`

Integrate explicit resource management when available in the runtime.

### 284. Support `Symbol.asyncDispose`

Release asynchronous resources through the standard protocol.

### 285. Implement Initialization Hook

Call `onInit` after dependencies are created.

### 286. Implement Destruction Hook

Call `onDestroy` before final release of the instance.

### 287. Define Lifecycle Hook Precedence

Record the order of decorators, interfaces, and standard symbols.

### 288. Call Initialization in Dependency Order

Initialize a dependency before the provider that consumes it.

### 289. Call Disposal in Reverse Order

Release dependents before dependencies.

### 290. Track Creation Order

Store the exact sequence of successfully created instances.

### 291. Do Not Destroy ValueProvider Automatically

Require an explicit ownership flag for external instances.

### 292. Implement Provider Ownership

Separate container-owned and externally owned resources.

### 293. Implement Disposal Timeout

Do not allow one hook to block shutdown indefinitely.

### 294. Pass AbortSignal to Disposal

Allow forced termination of long cleanup.

### 295. Handle Multiple Disposal Errors

Collect an AggregateError without stopping cleanup of the remaining instances.

### 296. Make Disposal Idempotent

Do not invoke cleanup repeatedly for one instance.

### 297. Implement Partial Graph Disposal

Release a selected provider and container-owned dependents.

### 298. Handle Reset Lifecycle

Destroy cached instances first, then allow recreation.

### 299. Integrate Process Signals

Correctly close the container on SIGTERM and SIGINT.

### 300. Test Lifecycle Hooks

Verify order, async cleanup, failures, ownership, and idempotency.

## 16. Error Model and Diagnostics

### 301. Create Base InjectraError

Add code, message, token, path, metadata, and cause.

### 302. Create ProviderNotFoundError

Show the missing token and dependency chain.

### 303. Create DuplicateProviderError

Show conflicting registrations and source modules.

### 304. Create AmbiguousProviderError

Show candidate providers and the way to fix the issue.

### 305. Create CircularDependencyError

Show the cycle path.

### 306. Create InvalidProviderError

Show a provider schema violation.

### 307. Create ScopeMismatchError

Show the captive dependency and lifecycles.

### 308. Create MissingScopeError

Show the required scope and root resolution.

### 309. Create AsyncResolutionError

Show an async dependency inside synchronous resolve.

### 310. Create ContainerDisposedError

Prohibit operations on a disposed container.

### 311. Create ContainerFrozenError

Prohibit late registrations.

### 312. Create LifecycleHookError

Preserve the hook name, provider, and original cause.

### 313. Create MetadataError

Show missing or ambiguous decorator metadata.

### 314. Create ModuleVisibilityError

Show the private provider and import/export chain.

### 315. Implement Error Formatting

Create a short message and an extended diagnostic report.

### 316. Implement Error Serialization

Return a safe JSON representation without instance values and secrets.

### 317. Add Resolution Trace

Record the sequence of registry lookup, cache hit, and instance creation.

### 318. Implement Debug Mode

Enable extended diagnostics without changing resolution semantics.

### 319. Implement Diagnostic Listeners

Publish registration, resolution, cache, and lifecycle events.

### 320. Test Error Stability

Record error codes and key diagnostic fields as public API.

## 17. Introspection and Graph Tooling

### 321. Implement Provider Inspection

Return token, kind, scope, dependencies, module, and status.

### 322. Implement Container Inspection

Show registrations, cached instances, and active scopes.

### 323. Do Not Expose Provider Values

Return metadata without secrets and internal object state.

### 324. Implement Dependency Graph Export

Export nodes and edges to JSON.

### 325. Implement Graphviz DOT Export

Generate a dependency graph diagram.

### 326. Implement Mermaid Export

Generate a diagram for Markdown documentation.

### 327. Highlight Scopes in Graph

Show singleton, transient, request, and custom lifecycles.

### 328. Highlight Module Boundaries

Group providers by modules.

### 329. Highlight Missing Dependencies

Show unresolved graph edges.

### 330. Highlight Circular Dependencies

Highlight strongly connected components.

### 331. Highlight Captive Dependencies

Mark scope lifetime violations.

### 332. Implement Graph Diff

Compare container configurations of two application versions.

### 333. Implement Provider Usage Analysis

Show roots, consumers, and resolution count.

### 334. Implement Unused Provider Report

Find registrations unused by the selected roots.

### 335. Implement Startup Timeline

Show the initialization duration of each eager provider.

### 336. Implement Resolution Timeline

Show nested duration of factory and constructor calls.

### 337. Implement Cache Statistics

Collect hit, miss, create, and reset counters.

### 338. Implement CLI `injectra inspect`

Print provider and module metadata.

### 339. Implement CLI `injectra graph`

Generate a JSON, DOT, or Mermaid graph.

### 340. Implement CLI `injectra validate`

Check registrations without launching the application.

## 18. Interceptors, Hooks, and Extensibility

### 341. Define ContainerPlugin Interface

Allow extension of registration, resolution, and lifecycle phases.

### 342. Implement Registration Hook

Call a plugin when a normalized provider is added.

### 343. Implement Before-resolve Hook

Pass the token and resolution context before lookup.

### 344. Implement After-resolve Hook

Pass resolved instance metadata without necessarily exposing the value.

### 345. Implement Before-create Hook

Allow instrumentation to measure factory or constructor invocation.

### 346. Implement After-create Hook

Publish duration and provider status.

### 347. Implement Resolution Middleware

Create a controlled chain around provider creation.

### 348. Limit Middleware Mutation

Do not allow a plugin to silently change token identity and scope rules.

### 349. Implement Provider Transformer

Allow build-time or bootstrap-time descriptor transformation.

### 350. Implement Instance Decorator

Wrap an instance through explicit provider configuration.

### 351. Research Method Interception

Create an optional Proxy-based AOP experiment.

### 352. Implement Logging Interceptor Example

Log method duration without changing the business class.

### 353. Implement Transaction Interceptor Example

Open a transaction around an annotated application method.

### 354. Record AOP Limitations

Document private fields, identity, stack traces, and performance overhead.

### 355. Implement Plugin Ordering

Use priority and a deterministic sequence.

### 356. Implement Plugin Isolation

Do not allow failure of an optional diagnostic plugin to break resolution.

### 357. Implement Critical Plugin Mode

Stop the container on failure of a security or validation plugin.

### 358. Implement Plugin Disposal

Release extension resources together with the container.

### 359. Create OpenTelemetry Plugin

Trace provider resolution and initialization.

### 360. Test Plugin API

Verify ordering, errors, async hooks, and disposal.

## 19. Testing Utilities

### 361. Create TestContainer

Add simplified configuration and automatic cleanup.

### 362. Implement Provider Override

Replace a production dependency with a test double.

### 363. Implement Value Stub

Register a plain object as a typed test dependency.

### 364. Implement Factory Spy

Track the number and order of provider creation.

### 365. Implement Constructor Spy

Check lifecycle without changing the production class.

### 366. Implement Resolution Assertions

Check that a token resolves to the expected implementation.

### 367. Implement Scope Assertions

Check instance equality between resolutions and scopes.

### 368. Implement Dependency Assertions

Check direct and transitive graph edges.

### 369. Implement No-cycle Assertion

Check for absence of circular dependencies.

### 370. Implement No-captive-dependency Assertion

Check lifecycle compatibility.

### 371. Implement Module-boundary Assertion

Check imports, exports, and private providers.

### 372. Implement Disposal Assertions

Check cleanup hook calls.

### 373. Implement Snapshot Graph Testing

Compare the dependency graph with a stored snapshot.

### 374. Implement Isolated Scope Helper

Automatically create and close a request or job scope.

### 375. Implement Fake Clock Provider

Test lifecycle timeout and expiration.

### 376. Implement Fake Configuration Provider

Pass deterministic environment values.

### 377. Implement Auto-mock Experiment

Generate basic mocks for missing dependencies.

### 378. Limit Auto-mocking

Do not hide missing critical providers by default.

### 379. Implement Test Leak Detection

Check for unclosed scopes and undisposed instances after a test.

### 380. Document Testing Patterns

Show unit tests without a container and integration tests with TestContainer.

## 20. Full Test Suite and Correctness

### 381. Create Token Model Tests

Verify identity, aliases, optional, lazy, and multi-tokens.

### 382. Create Provider Registration Tests

Verify all provider kinds, overrides, and invalid descriptors.

### 383. Create Synchronous Resolution Tests

Verify class, value, factory, and alias graphs.

### 384. Create Asynchronous Resolution Tests

Verify async factories, concurrent calls, and rejected initialization.

### 385. Create Singleton Scope Tests

Verify single creation and cache reset.

### 386. Create Transient Scope Tests

Verify a new tree of instances on every resolution.

### 387. Create Request Scope Tests

Verify reuse inside a scope and isolation between scopes.

### 388. Create Resolution Scope Tests

Verify a diamond dependency graph.

### 389. Create Custom Scope Tests

Verify user-defined cache and disposal strategy.

### 390. Create Circular Dependency Tests

Verify direct, indirect, alias, and module cycles.

### 391. Create Decorator API Tests

Verify metadata, inheritance, and explicit token overrides.

### 392. Create Module System Tests

Verify imports, exports, private providers, and dynamic configuration.

### 393. Create Child Container Tests

Verify overrides, singleton ownership, and hierarchy disposal.

### 394. Create Lifecycle Tests

Verify initialization, rollback, disposal, and AggregateError.

### 395. Create Graph Validation Tests

Verify missing providers, ambiguity, and captive dependencies.

### 396. Create Concurrency Tests

Perform parallel resolution of singleton, async, and scoped providers.

### 397. Create Provider Graph Fuzz Tests

Generate random acyclic and cyclic dependency graphs.

### 398. Create Property-based Tests

Verify invariants of caching, disposal order, and graph resolution.

### 399. Create Memory Leak Tests

Check release of transient graphs and disposed scopes through WeakRef.

### 400. Create Compatibility Tests

Verify supported Node.js and TypeScript versions.

## 21. Performance, Integrations, and Production-style Scenarios

### 401. Define Performance Targets

Record registration time, bootstrap time, resolve latency, and memory overhead.

### 402. Create Direct Construction Baseline

Compare container resolution with manual `new`.

### 403. Create Singleton Resolution Benchmark

Measure cached lookup by class, symbol, and InjectionToken.

### 404. Create Transient Graph Benchmark

Measure creation of a deep object graph.

### 405. Create Decorator Metadata Benchmark

Compare reflection-based and explicit dependency resolution.

### 406. Create Async Provider Benchmark

Measure concurrent singleton initialization.

### 407. Create Request Scope Benchmark

Measure scope creation and disposal per HTTP request.

### 408. Create Large Graph Benchmark

Test validation and bootstrap of thousands of providers.

### 409. Optimize Registry Lookup

Compare Map structures, normalized descriptors, and alias indirection.

### 410. Optimize Metadata Cache

Do not repeatedly read constructor dependency metadata through reflection.

### 411. Optimize Graph Validation

Cache the validated graph until registrations change.

### 412. Optimize Error Path Allocation

Do not create heavy diagnostic objects during successful resolution.

### 413. Implement Express Integration

Create request-scope middleware and release it after the response.

### 414. Implement HTTP Server Example

Assemble controller, service, repository, logger, and request context through Injectra.

### 415. Implement Worker Application Example

Create a job scope for each background task.

### 416. Implement Hexagonal Architecture Example

Bind application ports to PostgreSQL, Redis, and messaging adapters.

### 417. Implement Module Replacement Scenario

Switch between in-memory and production adapters without changing the application layer.

### 418. Implement Production Shutdown Scenario

Correctly shut down the HTTP server, database pool, Redis, and message consumers.

### 419. Create Architecture Documentation

Add C4 diagrams, dependency graph, lifecycle diagrams, ADR, and public API reference.

### 420. Prepare Production Readiness Checklist

Record requirements for API stability, scopes, async initialization, diagnostics, performance, testing, compatibility, and lifecycle safety.
