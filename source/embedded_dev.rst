How embedded development works
==============================

This chapter takes a look at the development of an Embedded System from the
perspective of a software developer.

Embedded Development usually is a cycle of
thesis -> implement -> try -> conclusion.
During this cycle a lot of different versions of a software have to be
deployed to an Embedded System.
To ease this process most of the *try* step happens automated:
Software is deployed automatically to a target, the target is booted into a
specific state and some tests are performed (by hand or automated).

In a perfect world the complete development cycle is accompanied by automated
testing on real hardware.

Most Embedded Systems are build for a special purpose:
They have defined interfaces for a user, for communication, measurement and
manipulation.
In addition to this product specific interfaces more interfaces are needed
for commissioning, development and production.

In the same way a PCB-designer adds test points to test the electronics during
production additional interfaces are needed for software development.
Since these interfaces are usually not needed - or even not wanted - in the
final product they can be done in a very lightweight way.

The following chapter will take a closer look at typically needed interfaces.
