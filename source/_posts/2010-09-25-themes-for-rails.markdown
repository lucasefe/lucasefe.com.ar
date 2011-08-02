---
layout: post
title: "Themes for Rails"
date: 2010-09-25 18:27
comments: true
categories: 
- ruby
- rails
- spanish
---

Ha pasado un buen tiempo desde mi &uacute;ltimo post. Soy uno m&aacute;s de los que abandona su blog cuando anda con muchas cosas, evidentemente. 

Para un laburo que estoy haciendo ahora (que espero no tardar en presentar) estaba necesitando soporte para themes. Mir&eacute; un poco por ah&iacute;, y di con [themes_support](http://github.com/jystewart/theme_support). Lamentablemente no ten&iacute;a soporte para Rails 3. Mirando un poco m&aacute;s me di cuenta de que estaba implementado usando t&eacute;cnicas de monkey patching (not a big fan) y que ya no le estaban dando mucha bola. Contact&eacute; al mantainer y lo consult&eacute; respecto al mantenimiento, y sobre una nueva versi&oacute;n para Rails3. Me dijo que no ten&iacute;a tiempo.  

Dado que realmente necesitaba algo para brindar dicha funcionalidad, decid&iacute; escribirla de cero, por mi cuenta. Esta nueva versi&oacute;n se "engancha" elegantemente de Rails 3, y ha sido testeada "bastante". Debo confezar que por primera vez us&eacute; TestUnit (antes era 100% rspec). Estuvo bueno. 

El c&oacute;digo se encuentra aqu&iacute;: [ThemesForRails]( 'http://github.com/lucasefe/themes_for_rails)

## Compatibilidad, Instalaci&oacute;n y el resto de la fruta:

Para simplificar, se usa exactamente  igual que el theme_support, aunque su instalaci&oacute;n es a trav&eacute;s de rubygems. Requiere Rails 3, obviamente. El readme cuenta con un mont&oacute;n de informaci&oacute;n.  

En fin, espero que a alguien le pueda servir tanto como a mi. 

Salud, Rubyistas. Nos vemos en [Uruguay](http://rubyconfuruguay.org/en), no?

