.. _language-server:

==================================
 Language Server Protocol Support
==================================

The Language Server Protocol allows text editors and IDEs to provide
features such as completion for a given (programming) language by
cooperating with a "language server" for the language in question that
is independent of the editor or IDE and can be use by any editor or
IDE. The :program:`build-generator` provides this functionality for
the various recipe languages it can process. This functionality is
available using the ``build-generator language-server`` sub-command.

Emacs
=====

Language Server Protocol support for Emacs can use the ``lsp-mode``
package.

The language server and Emacs side of the code can be downloaded here:

* https://jenkins-cse.bob.ci.cit-ec.net/job/build-generator-wip-language-server-ci-docker-build-generator-experiments/lastSuccessfulBuild/artifact/install/bin/build-generator

* https://raw.githubusercontent.com/RDTK/generator/wip-language-server/emacs-lisp/lsp-build-generator.el

The recommended setup requires the following packages

#. Add the "Melpa" package repository using ``M-x customize-option RET
   package-archives RET``, then adding ``melpa``, https://stable.melpa.org/packages/

#. ``M-x package-refresh-contents RET``

#. ``M-x install-package RET use-package RET``

The customization variable ``lsp-build-generator-program`` should be
use to configure the location of the ``build-generator`` program.

The following snippet applies the recommended configuration:

.. code-block:: emacs-lisp

   (use-package yaml-mode :ensure t)

   (use-package company :ensure t)

   (use-package lsp-mode :ensure t)
   (use-package lsp-ui :ensure t)

   (load "~/lsp-build-generator") ; Or wherever lsp-build-generator.el has been downloaded
   (setf lsp-build-generator-program "~/build-generator") ; Or wherever the build-generator binary has been downloaded

   (dolist (type '("template" "project" "distribution" "person"))
     (let ((hook-name (intern (concat type "-recipe-mode-hook"))))
       (add-hook hook-name
                 (lambda ()
                   (require 'company-capf)
                   (setf company-backends              '((company-capf))
                         company-minimum-prefix-length 1)

                   (lsp)

                   (require 'lsp-ui)
                   (lsp-ui-mode)))))

Vim
===

TODO

Visual Studio
=============

TODO
