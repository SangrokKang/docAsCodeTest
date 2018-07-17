---
ID: 206
post_title: Memory Manager
author: iamadmin
post_excerpt: ""
layout: post
permalink: http://10.177.230.99/wordpress/?p=206
published: true
post_date: 2018-07-17 16:40:43
---
<p class="BodyTxtNormal">Memory Manager는 시스템의 잔여 메모리 상태를 모니터링하고 관리하는 기능을 담당하는 모듈입니다.</p>
<p class="BodyTxtNormal">일반적으로 webOS의 앱은 사용자의 요청에 의해서 종료됩니다. 그러나 잔여 메모리 용량이 부족하게 되면 Memory Manager가 시스템이 강제로 앱을 종료시키게 됩니다.</p>

<h3 class="BodyTxtNormal" id="MemoryManager-메모리모니터링">메모리 모니터링</h3>
<p class="BodyTxtNormal"><strong>앱 실행을 위한 메모리 확보</strong></p>
<p class="BodyTxtNormal">Memory Manager는 앱을 실행하기 전에 필요한 메모리가 확보되었는지 확인합니다. 기본 요구 메모리는 120MB이며, 만일 메모리가 부족한 경우에는 백그라운드에 있는 앱을 종료시켜 필요한 만큼 메모리를 확보합니다.</p>
<p class="BodyTxtNormal"><strong>시스템 관리를 위한 메모리 확보</strong></p>
<p class="BodyTxtNormal">Memory Manager는 또한 동작 중 항상 87~119MB의 잔여 메모리를 유지하려고 합니다. 만일 잔여 메모리가 유지되지 않을 경우 역시 백그라운드에 실행 중인 앱을 종료시켜 메모리를 확보합니다.</p>
<p class="BodyTxtNormal">만일 더 이상 종료시킬 백그라운드 앱이 없으면 Memory Manager는 23~47MB의 잔여 메모리만을 유지합니다. 그러나 이 메모리도 유지할 수 없는 경우 Foreground에서 구동 중인 앱을 종료시키고 앱을 재실행합니다.</p>

<h3 class="BodyTxtNormal" id="MemoryManager-앱종료정책(KillAppPolicy?)">앱 종료 정책 (Kill App Policy?)</h3>
<p class="BodyTxtNormal">시스템 메모리의 부족으로 인해 앱을 강제 종료시킬 경우 아래와 같은 정책을 기반으로 종료시킬 앱을 선택합니다.</p>
<p class="BodyTxtNormal"><strong>Kill Preference Weight</strong></p>

<ul>
 	<li>
<ul>
 	<li class="BodyTxtListLv2">앱마다 0~100 사이의 Kill Preference Weight 값이 있으며, 값이 높은 앱이 먼저 종료될 가능성이 높습니다. Weight 값이 0인 앱은 종료되지 않습니다. Kill Preference Weight는 memorymanager-conf.json에 저장되어 있습니다.</li>
 	<li class="BodyTxtListLv2">일반적으로 앱의 Default Kill Preference Weight는 50 입니다. KeepAlive Flag가 설정되어 있는 앱은 Weight가 40으로 설정되고, 그에 따라 상대적으로 앱이 종료될 가능성이 더 낮습니다.  KeepAlive Flag는 sam-conf.json에 저장되어 있습니다. (KeepAlive Flag가 설정된 앱은 아닌지?)</li>
</ul>
</li>
</ul>
<p class="BodyTxtList"><strong>Least Recently Used (LRU) 방식으로 종료 대상 선정</strong></p>

<ul>
 	<li>
<ul>
 	<li class="BodyTxtListLv2">Weight가 동일할 경우에는 LRU 방식으로 종료시킬 앱을 선정합니다.</li>
 	<li class="BodyTxtListLv2">Foreground 앱에 따라 LRU 리스트를 갱신해 가면서 최근에 적게 사용된 앱을 종료 대상으로 선정합니다. 아래 표에서 붉은색으로 표시된 앱이 종료 대상입니다.</li>
</ul>
</li>
</ul>
&nbsp;

<!--more-->