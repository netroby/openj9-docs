<!--
* Copyright (c) 2017, 2018 IBM Corp. and others
*
* This program and the accompanying materials are made
* available under the terms of the Eclipse Public License 2.0
* which accompanies this distribution and is available at
* https://www.eclipse.org/legal/epl-2.0/ or the Apache
* License, Version 2.0 which accompanies this distribution and
* is available at https://www.apache.org/licenses/LICENSE-2.0.
*
* This Source Code may also be made available under the
* following Secondary Licenses when the conditions for such
* availability set forth in the Eclipse Public License, v. 2.0
* are satisfied: GNU General Public License, version 2 with
* the GNU Classpath Exception [1] and GNU General Public
* License, version 2 with the OpenJDK Assembly Exception [2].
*
* [1] https://www.gnu.org/software/classpath/license.html
* [2] http://openjdk.java.net/legal/assembly-exception.html
*
* SPDX-License-Identifier: EPL-2.0 OR Apache-2.0 OR GPL-2.0 WITH
* Classpath-exception-2.0 OR LicenseRef-GPL-2.0 WITH Assembly-exception
-->

# Class Data Sharing

Sharing class data between JVMs improves start up performance and reduces memory footprint.

Start up performance is improved by placing classes that an application needs when initializing into a shared classes cache. The next time the
application runs, it takes much less time to start because the classes are already available. When you enable class data sharing, AOT compilation is also enabled by default, which dynamically compiles certain methods into AOT code at runtime. By using these features in combination, startup performance can be improved even further because the cached AOT code can be used to quickly enable native code performance for subsequent runs of your application.

Class data sharing is enabled by setting the `-Xshareclasses` option on the command line when you start your application. When specified, OpenJ9 automatically creates a memory mapped file that stores and shares the classes in memory. By default, OpenJ9 always shares both the bootstrap and application classes that are loaded by the default system class loader.

The shared classes cache is updated dynamically; When an application loads new classes, the JVM automatically stores them in the cache without any user intervention.

Memory footprint is reduced by sharing common classes between applications that run in separate Java VMs.

The [-Xshareclasses](xshareclasses.md) option is highly configurable, allowing you to specify where to create the cache, how much space to allocate for AOT code and more. You can also set the cache size by using the [-Xscmx](xscmx.md) option. 

## Support for custom class loaders

Classes are shared by the bootstrap class loader internally in the OpenJ9 VM. If you are using a custom class loader, you can use the Java Helper API to find and store classes in the shared class cache.

For more information, see [Using the Java Helper API](https://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.vm.80.doc/docs/shrc_pd_helper.html).

## Cache utilities

Several utilities are provided for managing active caches, which are invoked by specifying `-Xshareclasses` suboptions. These utilities control the following types of operations:

- Adjust the minimum and maximum amount of cache space reserved for AOT or JIT data.
- Adjust the soft maximum size of the cache.
- Create snapshots of a cache.
- Create a cache from a snapshot.
- Remove caches and cache snapshots.
- List all the compatible and incompatible caches and snapshots.
- For problem determination, invalidate and revalidate AOT methods that cause a failure in an application.
- For problem determination, provide information to analyze the contents of a shared classes cache.

For more information, see [-Xshareclasses](xshareclasses.md).

## See also

- [AOT compiler](aot.md)
- [Class Sharing](https://www.ibm.com/developerworks/java/library/j-ibmjava4/index.html)
- [Diagnosing class data sharing problems](https://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.vm.80.doc/docs/shrc_pd_intro.html)


<!-- ==== END OF TOPIC ==== shrc.md ==== -->
