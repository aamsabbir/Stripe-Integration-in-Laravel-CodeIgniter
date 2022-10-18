# Stripe Integration in Laravel/CodeIgniter
This is Laravel Stripe payment getaway
# 1. You have to install a php package for stripe following this command 
<strong>composer require stripe/stripe-php</strong>

<h4>You need a <b>secret key</b> of stripe account which account your payment will be in</h4>

# 2. Add this code in your function in Laravel Controller
	try {
            $stripe = new StripeClient('SECRET_KEY');
            //  add card information here by which user pay
            $card = $stripe->tokens->create([
                'card' => [
                    'number' => '4242424242424242',
                    'exp_month' => 10,
                    'exp_year' => 2023,
                    'cvc' => '314',
                ],
            ]);
            //  make payment here using card above
            $payment = $stripe->charges->create([
                'source' => $card->id,
                'amount' => 50*100,
                'currency' => 'usd',
            ]);

            if($payment->status == 'succeeded'):
                return response()->json([
                    'status' => 'success',
                    'message' => 'Your payment is successful'
                ]);
            elseif ($payment->status == 'pending'):
                return response()->json([
                    'status' => 'pending',
                    'message' => 'Your payment is pending'
                ]);
            else:
                return response()->json([
                    'status' => 'failed',
                    'message' => 'Your payment is failed'
                ]);
            endif;

        } catch (Exception $e){
            return response()->json([
                'message' => $e->getMessage()
            ]);
        }
# 3. Add this line (definitely ensure your stripe path) in your function in CodeIgniter Controller    
    require_once APPPATH.'libraries/stripe/vendor/autoload.php';
 <br>   
# 4. demo card
<ul>
    <li>Card no: 4242424242424242</li>
    <li>exp_month: 10</li>
    <li>exp_year: 2022</li>
    <li>cvc/cvv: 314</li>
</ul>


<strong>Hope, This will be worked for you. Thank You</strong>
