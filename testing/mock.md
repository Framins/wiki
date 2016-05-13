Mock
====

Mock Object 是個很有趣的東西。測試框架利用一些機制，建造了一個虛擬物件，然後去偽裝成某個對象物件，這叫 Mock 。

舉例來說，今天有個權限 class 裡，有個可以檢查會員是否有某些權限的 function ，它需要傳入 Member object 。可是 Member object 並不是這個 case 想測試的目標，但我知道這個 Member object 的行為 (e.g. `getId() ) ，這時，就是使用 Mock 的時機了。

測試框架可以建立一個具備 Member object 行為的虛擬物件，並可以測試被使用的行為，如「 Member object 可以依群組 id 得知是否有在某個群組，這個群組 id 應該要大於 0 」之行為，也可藉由 Mock 來測試。
