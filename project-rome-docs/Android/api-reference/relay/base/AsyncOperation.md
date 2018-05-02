---
title: AsyncOperation
description: An operation that has a future result of type T or a possible exception. This class is slightly simplified version of the android api level 24 CompletableFuture class

keywords: microsoft, windows, device relay, Android, Android api reference 
---

# AsyncOperation class

```
@Keep public class AsyncOperation<T> implements Future<T>
```

An operation that has a future result of type T or a possible exception. This class is slightly simplified version of the android api level 24 CompletableFuture class

Implements the standard {@link java.util.concurrent.Future Future} interface, and also provides basic continuation functionality. Please see https://developer.android.com/reference/java/util/concurrent/CompletableFuture.html for detailed information on the how to use this class.

The important differences between CompletableFuture and AsyncOperation are as follows:
1. AsyncOperation's default asynchronous executor is Executors.newCachedThreadPool(), whereas CompletableFuture uses ForkJoinPool.commonPool().
2. AsyncOperation lacks obtrudeException and obtrudeValue methods.

## Interfaces

### ResultBiConsumer
`@FunctionalInterface public interface ResultBiConsumer<T, U>`

Represents an action to be invoked after an AsyncOperation is done.

This is a functional interface equivalent to android's BiConsumer

### ResultConsumer
`@FunctionalInterface public interface ResultConsumer<T>`

Represents an action to be invoked after an AsyncOperation is done.

This is a functional interface equivalent to android's Consumer

### ResultBiFunction
`@FunctionalInterface public interface ResultBiFunction<T, U, R>`

Represents a function to be invoked after an AsyncOperation is done.

This is a functional interface equivalent to android's BiFunction

### ResultFunction
`@FunctionalInterface public interface ResultFunction<T, R>`

Represents a function to be invoked after an AsyncOperation is done.

This is a functional interface equivalent to android's Function

### Supplier
`@FunctionalInterface public interface Supplier<T>`

Represents a function that supplies a T value (not necessarily new/distinct) when asked.

This is a functional interface equivalent to android's Supplier

## Member classes

### CompletionException
`public static class CompletionException extends RuntimeException`

Unchecked exception that holds the exception that caused the operation to complete exceptionally.

Used like {@link java.util.concurrent.ExecutionException ExecutionException} except that it is unchecked so that it can propagate to dependent operations without needing to know the full set of exceptions / requiring all exception observing continuations to declare that they may throw the ExecutionException.

## Constructors

### AsyncOperation
`public AsyncOperation()`

Creates a new AsyncOperation

## Methods

### isDone
`@Override public boolean isDone()`

Checks if the future is done. The future is done when the result is set or an exception is set.

 * **Returns:** if the operation is done

### isCancelled
`@Override public boolean isCancelled()`

Checks if the future has been successfully cancelled.

 * **Returns:** if the operation is cancelled

### cancel
`@Override public boolean cancel(boolean mayInterruptIfRunning)`

Attempts to cancel the future and stop waiting for a result.

Cancelling an AsyncOperation causes any threads waiting for the future via get() to immediately receive a CancellationException. The operation execution is not interrupted, but any eventual result from a cancelled call will be ignored.

 * **Parameters:** `mayInterruptIfRunning` — ignored because operations cannot be interrupted.
 * **Returns:** true if the future was cancelled before it was completed; false if the future could

     not be cancelled because it was already completed.

### get
`@Override public T get() throws InterruptedException, ExecutionException, CancellationException`

Gets the future value, waiting if necessary until the future is done.

 * **Returns:** The result of the operation, or null for a successful but empty result.

### get
`@Override public T get(long timeout, @NonNull TimeUnit unit) throws InterruptedException, TimeoutException, ExecutionException, CancellationException`

Attempts to get the future value, waiting if necessary until the future is done or until a timeout.

 * **Returns:** The result, or null for a successful but empty result.

### join
`public T join() throws InterruptedException, CompletionException, CancellationException`

Gets the future value, waiting if necessary until the future is done. Unlike get() join throws a CompletionException if any exception occured in the process of completing this operation

 * **Returns:** The operation result, or null for a successful but empty result.

### getNow
`public final T getNow(T valueIfAbsent) throws CompletionException, CancellationException`

Gets the value of the operation immediately returning a passed in value if the operation is not yet complete.

 * **Parameters:** `valueIfAbsent` — default value to return if operation isn't complete
 * **Returns:** The operation result, null for a successful but empty result, or the passed in

     value if the operation is not yet complete.

### isCompletedExceptionally
`public boolean isCompletedExceptionally()`

Checks if the operation completed in any exceptional way (cancellation or completeExceptionally)

 * **Returns:** if the operation is completed in an exceptional way (cancellation or explicitly)

### getNumberOfDependents
`public int getNumberOfDependents()`

Gets an estimated number of operations that are dependent on this operation. This is not intended to be used for synchronization / scheduling purposes.

 * **Returns:** number of operations currently awaiting this operation to complete.

### complete
`public final void complete(T value)`

Completes this operate with a given value.

 * **Parameters:** `value` — The result of the operation, or null for a successful but empty result.

### completeExceptionally
`public final void completeExceptionally(@NonNull Throwable ex)`

Sets the exception that will be thrown when the future value is retrieved, and marks the future done.

 * **Parameters:** `ex` — Throwable with which to complete the operation.

### handleAsync
`public <U> AsyncOperation<U> handleAsync ( @NonNull AsyncOperation.ResultBiFunction<? super T, ? super Throwable, ? extends U> action, @NonNull Executor executor)`

The handle triumvirate of functions (handle(action), handleAsync(action), and handleAsync(action,Executor)) are the most basic continuation functions upon which the others are built. Upon successful or exceptional completion of this operation, the passed in action will be executed allowing both antecedent results and antecedent exceptions to be observed.

 * **Parameters:**
   * `action` — Function that will be executed upon completion of this operation
   * `executor` — Executor with which to execute the function
   * `<U>` — Return type of the Function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

###  handleAsync
`public <U> AsyncOperation<U> handleAsync (@NonNull AsyncOperation.ResultBiFunction<? super T, ? super Throwable, ? extends U> action)`

The handle triumvirate of functions (handle(action), handleAsync(action), and handleAsync(action,Executor)) are the most basic continuation functions upon which the others are built. Upon successful or exceptional completion of this operation, the passed in action will be executed allowing both antecedent results and antecedent exceptions to be observed.

 * **Parameters:**
   * `action` — Function that will be executed upon completion of this operation
   * `<U>` — Return type of the Function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

###  handle
`public <U> AsyncOperation<U> handle (@NonNull AsyncOperation.ResultBiFunction<? super T, ? super Throwable, ? extends U> action)`

The handle triumvirate of functions (handle(action), handleAsync(action), and handleAsync(action,Executor)) are the most basic continuation functions upon which the others are built. Upon successful or exceptional completion of this operation, the passed in action will be executed allowing both antecedent results and antecedent exceptions to be observed.

 * **Parameters:**
   * `action` — Function that will be executed upon completion of this operation
   * `<U>` — Return type of the Function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### whenCompleteAsync
`public AsyncOperation<T> whenCompleteAsync ( @NonNull AsyncOperation.ResultBiConsumer<? super T, ? super Throwable> action, @NonNull Executor executor)`

The whenComplete triumvirate of functions (whenComplete(action), whenCompleteAsync(action), and whenCompleteAsync(action,Executor)) are similar to the handle functions. Upon successful or exceptional completion of this operation, the passed in action will be executed allowing both antecedent results and antecedent exceptions to be observed. Unlike handle, the results of the action do not propagate to dependent operations; they observe this stage's exception / result instead of the passed in action's

 * **Parameters:**
   * `action` — Function that will be executed upon completion of this operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### whenCompleteAsync
`public AsyncOperation<T> whenCompleteAsync (@NonNull AsyncOperation.ResultBiConsumer<? super T, ? super Throwable> action)`

The whenComplete triumvirate of functions (whenComplete(action), whenCompleteAsync(action), and whenCompleteAsync(action,Executor)) are similar to the handle functions. Upon successful or exceptional completion of this operation, the passed in action will be executed allowing both antecedent results and antecedent exceptions to be observed. Unlike handle, the results of the action do not propagate to dependent operations; they observe this stage's exception / result instead of the passed in action's

 * **Parameters:** `action` — Function that will be executed upon completion of this operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### whenComplete
`public AsyncOperation<T> whenComplete (@NonNull AsyncOperation.ResultBiConsumer<? super T, ? super Throwable> action)`

The whenComplete triumvirate of functions (whenComplete(action), whenCompleteAsync(action), and whenCompleteAsync(action,Executor)) are similar to the handle functions. Upon successful or exceptional completion of this operation, the passed in action will be executed allowing both antecedent results and antecedent exceptions to be observed. Unlike handle, the results of the action do not propagate to dependent operations; they observe this stage's exception / result instead of the passed in action's

 * **Parameters:** `action` — Function that will be executed upon completion of this operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### exceptionally
`public AsyncOperation<T> exceptionally (@NonNull AsyncOperation.ResultFunction<Throwable, ? extends T> action)`

Allows continuations to be attached that only run in the case of an exceptional completion of this operation. Note that there are no *async* variants of exceptionally so the action should not be long running as it may be blocking the thread that completed this operation or the calling thread ( in the case of an already completed operation).

 * **Parameters:** `action` — the action to perform when the operation completes exceptionally.

### thenRunAsync
`public AsyncOperation<Void> thenRunAsync (@NonNull Runnable action, @NonNull Executor executor)`

The thenRun triumvirate of functions (thenRun(action), thenRunAsync(action), and thenRunAsync(action,Executor)) run a passed in Runnable when this operation completes successfully.

 * **Parameters:**
   * `action` — Runnable that will be executed upon completion of this operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenRunAsync
`public AsyncOperation<Void> thenRunAsync (@NonNull Runnable action)`

The thenRun triumvirate of functions (thenRun(action), thenRunAsync(action), and thenRunAsync(action,Executor)) run a passed in Runnable when this operation completes successfully.

 * **Parameters:** `action` — Runnable that will be executed upon completion of this operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenRun
`public AsyncOperation<Void> thenRun (@NonNull Runnable action)`

The thenRun triumvirate of functions (thenRun(action), thenRunAsync(action), and thenRunAsync(action,Executor)) run a passed in Runnable when this operation completes successfully.

 * **Parameters:** `action` — Runnable that will be executed upon completion of this operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenAcceptAsync
`public AsyncOperation<Void> thenAcceptAsync (@NonNull ResultConsumer<? super T> action, @NonNull Executor executor)`

The thenAccept triumvirate of functions (thenAcceptAsync(action), thenAcceptAsync(action), and thenAcceptAsync(action,Executor)) run a passed in ResultConsumer when this operation completes successfully.

 * **Parameters:**
   * `action` — ResultConsumer that will be executed upon completion of this operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenAcceptAsync
`public AsyncOperation<Void> thenAcceptAsync (@NonNull ResultConsumer<? super T> action)`

The thenAccept triumvirate of functions (thenAcceptAsync(action), thenAcceptAsync(action), and thenAcceptAsync(action,Executor)) run a passed in ResultConsumer when this operation completes successfully.

 * **Parameters:** `action` — ResultConsumer that will be executed upon completion of this operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenAccept
`public AsyncOperation<Void> thenAccept (@NonNull ResultConsumer<? super T> action)`

The thenAccept triumvirate of functions (thenAcceptAsync(action), thenAcceptAsync(action), and thenAcceptAsync(action,Executor)) run a passed in ResultConsumer when this operation completes successfully.

 * **Parameters:** `action` — ResultConsumer that will be executed upon completion of this operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

###  thenApplyAsync
`public <U> AsyncOperation<U> thenApplyAsync (@NonNull ResultFunction<? super T, ? extends U> action, @NonNull Executor executor)`

The thenApply triumvirate of functions (thenApplyAsync(action), thenApplyAsync(action), and thenApplyAsync(action,Executor)) run a passed in ResultFunction when this operation completes successfully.

 * **Parameters:**
   * `action` — ResultFunction that will be executed upon completion of this operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenApplyAsync
`public <U> AsyncOperation<U> thenApplyAsync (@NonNull ResultFunction<? super T, ? extends U> action)`

The thenApply triumvirate of functions (thenApplyAsync(action), thenApplyAsync(action), and thenApplyAsync(action,Executor)) run a passed in ResultFunction when this operation completes successfully.

 * **Parameters:** `action` — ResultFunction that will be executed upon completion of this operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenApply
`public <U> AsyncOperation<U> thenApply (@NonNull ResultFunction<? super T, ? extends U> action)`

The thenApply triumvirate of functions (thenApplyAsync(action), thenApplyAsync(action), and thenApplyAsync(action,Executor)) run a passed in ResultFunction when this operation completes successfully.

 * **Parameters:** `action` — ResultFunction that will be executed upon completion of this operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### acceptEitherAsync
`public AsyncOperation<Void> acceptEitherAsync ( @NonNull AsyncOperation<? extends T> other, AsyncOperation.ResultConsumer<? super T> action, @NonNull Executor executor)`

The acceptEither triumvirate of functions run a passed in ResultConsumer when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — ResultConsumer that will be executed upon completion of either operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### acceptEitherAsync
`public AsyncOperation<Void> acceptEitherAsync ( @NonNull AsyncOperation<? extends T> other, @NonNull AsyncOperation.ResultConsumer<? super T> action)`

The acceptEither triumvirate of functions run a passed in ResultConsumer when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — ResultConsumer that will be executed upon completion of either operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### acceptEither
`public AsyncOperation<Void> acceptEither ( @NonNull AsyncOperation<? extends T> other, @NonNull AsyncOperation.ResultConsumer<? super T> action)`

The acceptEither triumvirate of functions run a passed in ResultConsumer when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — ResultConsumer that will be executed upon completion of either operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action


### applyToEitherAsync
`public <U> AsyncOperation<U> applyToEitherAsync (@NonNull AsyncOperation<? extends T> other, @NonNull AsyncOperation.ResultFunction<? super T, U> action, @NonNull Executor executor)`

The applyToEither triumvirate of functions run a passed in ResultFunction when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — ResultFunction that will be executed upon completion of either operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### applyToEitherAsync
`public <U> AsyncOperation<U> applyToEitherAsync ( @NonNull AsyncOperation<? extends T> other, @NonNull AsyncOperation.ResultFunction<? super T, U> action)`

The applyToEither triumvirate of functions run a passed in ResultFunction when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — ResultFunction that will be executed upon completion of either operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### applyToEither
`public <U> AsyncOperation<U> applyToEither ( @NonNull AsyncOperation<? extends T> other, @NonNull AsyncOperation.ResultFunction<? super T, U> action)`

The applyToEither triumvirate of functions run a passed in ResultFunction when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — ResultFunction that will be executed upon completion of either operation
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### runAfterEitherAsync
`public AsyncOperation<Void> runAfterEitherAsync ( @NonNull AsyncOperation<?> other, @NonNull Runnable action, @NonNull Executor executor)`

The runAfterEither triumvirate of functions run a passed in Runnable when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — Runnable that will be executed upon completion of either operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### runAfterEitherAsync
`public AsyncOperation<Void> runAfterEitherAsync (@NonNull AsyncOperation<?> other, @NonNull Runnable action)`

The runAfterEither triumvirate of functions run a passed in Runnable when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — Runnable that will be executed upon completion of either operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### runAfterEither
`public AsyncOperation<Void> runAfterEither (@NonNull AsyncOperation<?> other, @NonNull Runnable action)`

The runAfterEither triumvirate of functions run a passed in Runnable when either this operation or the passed in operation completes successfully. If the operation that completes does so exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "OR" together
   * `action` — Runnable that will be executed upon completion of either operation
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenCombineAsync
`public <U, V> AsyncOperation<V> thenCombineAsync (@NonNull AsyncOperation<? extends U> other, @NonNull AsyncOperation.ResultBiFunction<? super T, ? super U, ? extends V> action, @NonNull Executor executor)`

The thenCombine triumvirate of functions run a passed in ResultFunction when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — ResultFunction that will be executed upon completion of both operations
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenCombineAsync
`public <U, V> AsyncOperation<V> thenCombineAsync ( @NonNull AsyncOperation<? extends U> other, @NonNull AsyncOperation.ResultBiFunction<? super T, ? super U, ? extends V> action)`

The thenCombine triumvirate of functions run a passed in ResultFunction when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — ResultFunction that will be executed upon completion of both operations
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenCombine
`public <U, V> AsyncOperation<V> thenCombine ( @NonNull AsyncOperation<? extends U> other, @NonNull AsyncOperation.ResultBiFunction<? super T, ? super U, ? extends V> action)`

The thenCombine triumvirate of functions run a passed in ResultFunction when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — ResultFunction that will be executed upon completion of both operations
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenAcceptBothAsync
`public <U> AsyncOperation<Void> thenAcceptBothAsync (@NonNull AsyncOperation<? extends U> other, @NonNull AsyncOperation.ResultBiConsumer<? super T, ? super U> action, @NonNull Executor executor)`

The thenAcceptBoth triumvirate of functions run a passed in ResultConsumer when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — ResultConsumer that will be executed upon completion of both operations
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenAcceptBothAsync
`public <U> AsyncOperation<Void> thenAcceptBothAsync ( @NonNull AsyncOperation<? extends U> other, @NonNull AsyncOperation.ResultBiConsumer<? super T, ? super U> action)`

The thenAcceptBoth triumvirate of functions run a passed in ResultConsumer when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — ResultConsumer that will be executed upon completion of both operations
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenAcceptBoth
`public <U> AsyncOperation<Void> thenAcceptBoth ( @NonNull AsyncOperation<? extends U> other, @NonNull AsyncOperation.ResultBiConsumer<? super T, ? super U> action)`

The thenAcceptBoth triumvirate of functions run a passed in ResultConsumer when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — ResultConsumer that will be executed upon completion of both operations
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### runAfterBothAsync
`public AsyncOperation<Void> runAfterBothAsync (@NonNull AsyncOperation<?> other, @NonNull Runnable action, @NonNull Executor executor)`

The runAfterBoth triumvirate of functions run a passed in Runnable when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — Runnable that will be executed upon completion of both operations
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### runAfterBothAsync
`public AsyncOperation<Void> runAfterBothAsync (@NonNull AsyncOperation<?> other, @NonNull Runnable action)`

The runAfterBoth triumvirate of functions run a passed in Runnable when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — Runnable that will be executed upon completion of both operations
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### runAfterBoth
`public AsyncOperation<Void> runAfterBoth (@NonNull AsyncOperation<?> other, @NonNull Runnable action)`

The runAfterBoth triumvirate of functions run a passed in Runnable when this operation and the passed in operation completes successfully. If either operation completes exceptionally, the returned operation also completes exceptionally.

 * **Parameters:**
   * `other` — the other operation to "AND" together
   * `action` — Runnable that will be executed upon completion of both operations
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenComposeAsync
`public <U> AsyncOperation<U> thenComposeAsync ( AsyncOperation.ResultFunction<? super T, ? extends AsyncOperation<U>> action, Executor executor)`

The thenCompose triumvirate of functions run a passed in ResultFunction when this operation completes successfully. The ResultFunction returns an AsyncOperation<T> and the return operation from this call returns a AsyncOperation<T> as opposed to a AsyncOperation<AsyncOperation<T>>

 * **Parameters:**
   * `action` — Function that will be executed upon completion of both operations
   * `executor` — Executor with which to execute the function
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenComposeAsync
`public <U> AsyncOperation<U> thenComposeAsync (@NonNull AsyncOperation.ResultFunction<? super T, ? extends AsyncOperation<U>> action)`

The thenCompose triumvirate of functions run a passed in ResultFunction when this operation completes successfully. The ResultFunction returns an AsyncOperation<T> and the return operation from this call returns a AsyncOperation<T> as opposed to a AsyncOperation<AsyncOperation<T>>

 * **Parameters:** `action` — Function that will be executed upon completion of both operations
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### thenCompose
`public <U> AsyncOperation<U> thenCompose (@NonNull AsyncOperation.ResultFunction<? super T, ? extends AsyncOperation<U>> action)`

The thenCompose triumvirate of functions run a passed in ResultFunction when this operation completes successfully. The ResultFunction returns an AsyncOperation<T> and the return operation from this call returns a AsyncOperation<T> as opposed to a AsyncOperation<AsyncOperation<T>>

 * **Parameters:** `action` — Function that will be executed upon completion of both operations
 * **Returns:** A new async operation that will complete based on the outcome of passed in action

### completedFuture
`public static <U> AsyncOperation<U> completedFuture (U value)`

Creates an operation that is already completed with the given value

 * **Parameters:** `value` — value with which to complete the operation
 * **Returns:** A new async operation that is already completed

### runAsync
`public static AsyncOperation<Void> runAsync (@NonNull Runnable runnable)`

Creates an operation that will run the passed in Runnable on the default executor

 * **Parameters:** `runnable` — action to run
 * **Returns:** A new async operation that will complete when the runnable completes

### runAsync
`public static AsyncOperation<Void> runAsync (@NonNull Runnable runnable, @NonNull Executor executor)`

Creates an operation that will run the passed in Runnable on the passed in executor

 * **Parameters:**
   * `runnable` — action to run
   * `executor` — executor on which to run the action
 * **Returns:** A new async operation that will complete when the runnable completes

### supplyAsync
`public static <U> AsyncOperation<U> supplyAsync (@NonNull AsyncOperation.Supplier<U> supplier, @NonNull Executor executor)`

Creates an operation that will use the passed in executor to get a value from the supplier

 * **Parameters:**
   * `supplier` — supplier from which to get a value to complete this operation
   * `executor` — executor on which to run the action
 * **Returns:** A new async operation that will complete with a value from the supplier

### supplyAsync
`public static <U> AsyncOperation<U> supplyAsync (@NonNull AsyncOperation.Supplier<U> supplier)`

Creates an operation that will use the default executor to get a value from the supplier

 * **Parameters:** `supplier` — supplier from which to get a value to complete this operation
 * **Returns:** A new async operation that will complete with a value from the supplier

### allOf
`public static AsyncOperation<Void> allOf (@NonNull AsyncOperation<?>... operations)`

Creates an operation that will complete when all of the passed operations complete.

 * **Parameters:** `operations` — list of operations to "AND" together
 * **Returns:** A new async operation that will complete when all operations complete

### anyOf
`public static AsyncOperation<Object> anyOf (@NonNull AsyncOperation<?>... operations)`

Creates an operation that will complete when any of the passed operations complete.

 * **Parameters:** `operations` — list of operations to "OR" together
 * **Returns:** A new async operation that will complete when any operations complete


## Example

The following sample code sets up the initialization of a Platform instance, using the AsyncOperation class to handle the result. 

```Java
ApplicationRegistrationBuilder registrationBuilder = new ApplicationRegistrationBuilder();

// add app-specific attributes here
registrationBuilder.addAttribute("Attribute", "value");

ApplicationRegistration applicationRegistration = registrationBuilder.buildRegistration();

// Instantiate Platform using the UserAccountProvider the sign-in helper provides
// NotificationProvider is used for hosting capabilities (optional), so we pass in null
AsyncOperation<PlatformCreationResult> resultOperation = Platform.createInstanceAsync(
        this, null, applicationRegistration, getSignInHelper());

// Can handle success/failure to create platform, simply give a toast
resultOperation.whenCompleteAsync(new AsyncOperation.ResultBiConsumer<PlatformCreationResult, Throwable>()
{
        @Override
        public void accept(PlatformCreationResult platformCreationResult, Throwable throwable) throws Throwable
        {
        Log.d("accept", "Entered accept");
        if (throwable != null)
                return;

        if (platformCreationResult.getStatus() == PlatformCreationStatus.FAILURE)
                return;

        // save instance of successfully created Platform
        mPlatform = platformCreationResult.getPlatform();
        mPlatformInitialized = true;

        }
});
```