---
title: AssertFalse
summary: Assertions may be disabled at runtime and do not guarantee that execution will halt here; consider throwing an exception instead
layout: bugpattern
category: JDK
severity: WARNING
maturity: EXPERIMENTAL
---

<!--
*** AUTO-GENERATED, DO NOT MODIFY ***
To make changes, edit the @BugPattern annotation or the explanation in docs/bugpattern.
-->

## The problem
Java assertions do not necessarily execute at runtime; they may be enabled and disabled depending on which options are passed to the JVM invocation. An assert false statement may be intended to ensure that the program never proceeds beyond that statement. If the correct execution of the program depends on that being the case, consider throwing an exception instead, so that execution is halted regardless of runtime configuration.

## Suppression
Suppress false positives by adding an `@SuppressWarnings("AssertFalse")` annotation to the enclosing element.

----------

## Examples
__AssertFalseNegativeCases.java__

{% highlight java %}
/*
 * Copyright 2015 Google Inc. All Rights Reserved.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package com.google.errorprone.bugpatterns;

/**
 * @author sebastian.h.monte@gmail.com (Sebastian Monte)
 */
public class AssertFalseNegativeCases {

  public void assertTrue() {
    assert true;
  }

  public void assertFalseFromCondition() {
    assert 0 == 1;
  }
}
{% endhighlight %}

__AssertFalsePositiveCases.java__

{% highlight java %}
/*
 * Copyright 2015 Google Inc. All Rights Reserved.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package com.google.errorprone.bugpatterns;

/**
 * @author sebastian.h.monte@gmail.com (Sebastian Monte)
 */
public class AssertFalsePositiveCases {
  public void assertFalse() {
    // BUG: Diagnostic contains: throw new AssertionError()
    assert false;
  }
}
{% endhighlight %}
