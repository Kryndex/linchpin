libvirt
=======

The libvirt provider manages two types of resources.

.. _libvirt_node:

libvirt_node
------------

Libvirt Domains (or nodes) can be provisioned using this resource.

* :docs1.5:`Topology Example <workspace/topologies/libvirt-new.yml>`
* `Ansible module <http://docs.ansible.com/ansible/latest/virt_module.html>`_

.. _libvirt_network:

libvirt_network
---------------

Libvirt networks can be provisioned. If a :ref:`libvirt_network` is to be used with a :ref:`libvirt_node`, it must precede it.

* :docs1.5:`Topology Example <workspace/topologies/libvirt-el7net.yml>`
* `Ansible module <http://docs.ansible.com/ansible/latest/virt_net_module.html>`_

.. note:: This resource will not be torn down during a :term:`destroy`
   action. This is because other resources may depend on the now existing
   resource.

Additional Dependencies
-----------------------

The libvirt resource group requires several additional dependencies. The
following must be installed.

* libvirt-devel
* libguestfs-tools
* python-libguestfs
* libvirt-python
* python-lxml

For a Fedora 26 machine, the dependencies would be installed using dnf.

.. code-block:: bash

  $ sudo dnf install libvirt-devel libguestfs-tools python-libguestfs
  $ pip install linchpin[libvirt]

Additionally, because libvirt downloads images, certain SELinux libraries must
exist.

* libselinux-python

For a Fedora 26 machine, the dependencies would be installed using dnf.

.. code-block:: bash

  $ sudo dnf install libselinux-python

If using a python virtual environment, the selinux libraries must be symlinked. Assuming
a virtualenv of ``~/venv``, symlink the libraries.

.. code-block:: bash

  $ export LIBSELINUX_PATH=/usr/lib64/python2.7/site-packages
  $ ln -s ${LIBSELINUX_PATH}/selinux ~/venv/lib/python2.7/site-packages
  $ ln -s ${LIBSELINUX_PATH}/_selinux.so ~/venv/lib/python2.7/site-packages

Credentials Management
----------------------

Libvirt doesn't require credentials via LinchPin. Multiple options are
available for authenticating against a Libvirt daemon (libvirtd). Most methods
are detailed `here <https://libvirt.org/auth.html>`_.  If desired, the uri for
the resource can be set using one of these mechanisms.
