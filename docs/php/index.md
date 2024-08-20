---
layout: post
title:  PHP
date:   2022-06-24 20:31:00 +0800
categories: php doc
has_children: true
nav_order: 1
---

# PHP

1. Imagick 扩展的权限策略
	```shell
	# Uncomment

	<policy domain="coder" rights="read|write" pattern="{GIF,JPEG,PNG,WEBP}" />

	# Add this line inside <policymap>

	<policy domain="module" rights="read|write" pattern="{PS,PDF,XPS}" />

	# Comment these lines:

	  <!--
	  <policy domain="coder" rights="none" pattern="PS" />
	  <policy domain="coder" rights="none" pattern="PS2" />
	  <policy domain="coder" rights="none" pattern="PS3" />
	  <policy domain="coder" rights="none" pattern="EPS" />
	  <policy domain="coder" rights="none" pattern="PDF" />
	  <policy domain="coder" rights="none" pattern="XPS" />
	   -->
	```